# Frequently Asked Questions

### Question: How do I contribute to ShopifySharp?

[Check out our contribution guide!](https://github.com/nozzlegear/ShopifySharp/blob/master/docs/contribution-guide.md) Is the guide missing anything? Please let me know by opening an issue!

### Question: How do I look up a Shopify order by its name?

[See this article to learn how to look up a Shopify order by its name property.](https://nozzlegear.com/shopify/looking-up-a-shopify-order-by-its-name)

### Question: How do I use ShopifySharp with a private app?

ShopifySharp works with any private Shopify app, no extra configuration needed. All you need to do is pass in your private app's password wherever ShopifySharp asks for an access token. For example: `var service = new ShopifySharp.OrderService("mydomain.myshopify.com", "PRIVATE APP PASSWORD HERE")`. This package's test suite uses a private app for testing API calls, so this method is confirmed working.

### Question: X method or Y endpoint randomly 404s/throws exceptions for some shops.

Make sure that you're always using a \*.myshopify.com domain! While a "real" domain like "example.com" will often work with the API, there are some API endpoints that will randomly return redirects or 404s if you aren't using the \*.myshopify.com domain. [See this post by @dnatabar](https://github.com/nozzlegear/ShopifySharp/issues/286#issuecomment-1248952763) and [this post by @flgatormike](https://github.com/nozzlegear/ShopifySharp/issues/723#issuecomment-1074623062) for more information.

### Question: Updating a product (or other object) unpublishes it?

This is an issue related to the serialization of default property values in dotnet. As developers, we often want to update only a small subset of properties on an object. However, any property that is not explicitly given a value in dotnet will instead be initialized and serialized with its default value. 

For the `Product.PublishedAt` property, this default value is `null`. Setting `PublishedAt` to `null` will **unpublish** the product, removing it from the storefront and making it unavailable for puchase. The fix is to first pull in the product with the API and then update its properties.

```cs
var product = await productService.GetAsync(productId);
product.SomeProperty = newValue;
product = await productService.UpdateAsync(productId, product);
```

We're looking for feedback on methods to improve object updating and property serialization in ShopifySharp. [You can offer feedback here](https://github.com/nozzlegear/ShopifySharp/issues/388), and check out these issues ([#284](https://github.com/nozzlegear/ShopifySharp/issues/284), [#367](https://github.com/nozzlegear/ShopifySharp/issues/367), [#373](https://github.com/nozzlegear/ShopifySharp/issues/373), [#379](https://github.com/nozzlegear/ShopifySharp/issues/379), [#642](https://github.com/nozzlegear/ShopifySharp/issues/642)) for further history on the problem.

### Question: How can I use ShopifySharp with Dependency Injection?

Install the [ShopifySharp.Extensions.DependencyInjection package from Nuget](https://nuget.org/packages/ShopifySharp.Extensions.DependencyInjection), which adds support for injecting ShopifySharp services into .NET classes using Microsoft's Dependency Injection framework. To do this, it exposes several methods that extend the [IServiceCollection interface](https://learn.microsoft.com/en-us/dotnet/api/microsoft.extensions.dependencyinjection.iservicecollection?view=dotnet-plat-ext-8.0). Microsoft's DI framework will then make the ShopifySharp services available to the rest of your code when you add the interfaces to your class constructors.

```cs
// In your Program.cs or Startup.cs file, or wherever you register your Dependency Injection services
public class DependencyInjectionExample(IServiceCollection services)
{
    // ...
    
    // Add ShopifySharp's service factories and the LeakyBucketExecutionPolicy to your DI container
    services.AddShopifySharp<LeakyBucketExecutionPolicy>(options =>
    {
        options.RequestExecutionPolicy = new LeakyBucketExecutionPolicy(); 
    });
}

// In the class where you want to use a ShopifySharp service
public class MyClass(IOrderServiceFactory orderServiceFactory)
{
    public async Task ListOrdersForUser()
    {
        var user = await DoSomethingToGetUser();
        var credentials = new ShopifyRestApiCredentials(user.ShopDomain, user.AccessToken);
        var orderService = orderServiceFactory.Create(credentials);
        
        // Because the service was created using the injected factory class, 
        // it's automatically using the LeakyBucket request policy. That means it will
        // gracefully handle Shopify's API request limit and will wait if it hits the
        // limit (instead of throwing an exception).
        var orders = await ordrService.ListAsync();
    }
}
```

Check the [package's documentation](./ShopifySharp.Extensions.DependencyInjection/README.md) for more information.


# "Why don't you use enums?"

I'm a big fan of using enums to make things easier for C# devs, because it removes a lot of the headache that comes with trying to remember all the valid string options for certain properties. With enums, we get those options hardcoded by default. We can easily scroll up and down the list of known values and select the one we need, without having to worry about typos.

Many Shopify objects have string properties that only accept a predetermined list of values, and these properties are perfect for matching to C# enums. Unfortunately, Shopify has a habit of only documenting the most used values and leaving the developer to guess the rest. On top of that, they sometimes change those enums completely, [such as this case where they changed the enums used for filtering orders without announcing it](https://github.com/nozzlegear/ShopifySharp/issues/64).

That's a problem when it comes to strongly-typed languages like C#. If you receive an enum property that doesn't have a value matching the enum, you're going to get a big fat exception thrown in your face. This is especially problematic when these undocumented enum values are sent to you automatically in webhooks.

On top of that, if there's an enum value that you need to send but isn't in ShopifySharp, you'll need to wait until a new version of the lib is released before you can use it.

Enums would be much better suited to ShopifySharp if Shopify themselves used API versioning, but sadly that isn't the case. After struggling with undocumented values and unannounced changes that break apps through two major releases of ShopifySharp, I've made the decision to pull the plug on almost all enums in the lib.

What were previously enums in ShopifySharp 1.x and 2.x are now string properties. This change will prevent breaking your app when an enum value changes, and will allow you to quickly update your app when a new enum value is released without waiting on an update to ShopifySharp first.


