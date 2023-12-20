
# Handling Shopify's API rate limit

The Shopify API allows for an average of 2 API calls per second, with a burst limit of up to 40 API calls. Once you hit that 40 burst limit, Shopify will return a 429 Too Many Requests result. The limit is there to prevent you and thousands of other developers from overloading Shopify's servers by going hard in the paint with hundreds of requests every second. Unfortunately, it's pretty easy to write a `for` loop while trying to close a list of orders, and then start getting exceptions after closing the first 40.

By default, ShopifySharp will **not** retry requests that get throttled by the rate limit, and instead this package will throw a `ShopifyRateLimitException` that you can catch and decide to retry:

```cs
foreach (var order in listOfOrders)
{
	try
	{
		await orderService.CloseAsync(order.Id.Value);
	}
	catch (ShopifyRateLimitException e)
	{
		//Wait for 10 seconds before trying again.
		await Task.Delay(10000);

		//If this throws an exception again, loop will break and the exception will be thrown.
		await orderService.CloseAsync(order.Id.Value);
	}
}
```