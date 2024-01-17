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