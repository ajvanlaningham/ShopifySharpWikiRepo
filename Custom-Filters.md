# Custom Filters

Occasionally we get requests to add certain properties to one of the List or Count filters that isn't documented anywhere by Shopify. For example, at one point it was possible to add a `name` prop to the `OrderFilter` that would make it possible to search for an `Order` by its name. Unfortunately this `name` filter was never documented and Shopify eventually removed that functionality, but it's a perfect example of wanting to use custom properties on the filters.

Officially, my stance is that I tend to favor not adding undocumented things to this package on the fear that it will someday break and I'll have a big headache fielding questions and issues here on GitHub when it does. However, in the case of Filters it's possible for you to implement your own custom filter without it being officially supported!

It's as easy as creating your own class that extends whichever filter your method accepts. For example, let's pretend that `name` search still works when listing Shopify orders, but this package doesn't support it. The `OrderService.ListAsync` method accepts an `OrderFilter` argument, so to get the `name` property sent along with the API call, all you need to do is create your own custom filter that extends `OrderFilter`:

```cs
public class MyCustomOrderFilter : OrderFilter
{
    [JsonProperty("name")] // This will serialize the value as `name` when sent to the API endpoint.
    public string Name { get; set; }
}
```

Your custom order filter still has all of the original properties of the base `OrderFilter` class, _plus_ it has your new `Name` property. Since your custom filter extends the class that `OrderService.ListAsync` was looking for, you can now pass it as an argument to that method without any problems:

```cs
var list = await orderService.ListAsync(new MyCustomOrderFilter()
{
    Name = "1001"
});
```

If you need even more fine-grained control over what gets sent through your custom filter, you can also override the `ToParameters` or `ToSingleParameter` methods of the filter. Those methods are called by the service when it's serializing the filter to a querystring.

[You can take a look at the `Parameterizable` class (which is used by all filters) for a look at the current implementation](https://github.com/nozzlegear/ShopifySharp/blob/85a0eed28937eee2870e9104a55796e1a1039cfb/ShopifySharp/Infrastructure/Parameterizable.cs#L18) and what you can do in those methods.


