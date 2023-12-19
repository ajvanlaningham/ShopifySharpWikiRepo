## Checkouts

If you're building an app with the Sales Channel SDK, then you can use the Checkout API to let customers purchase products from Shopify stores that have installed your sales channel.

Shopify uses the Checkout resource to manage a user's cart as it transitions to a paid order. This process includes specifying which line items are included in the checkout, attaching a customer's shipping and payment details, and calculating tax and shipping rates. Credit card payments can be attached to a Checkout using the Payment resource.

### Create Checkouts

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var checkout = await service.CreateAsync(new Checkout
{
    Email = "joshua@nozzlegear.com"
});
```

### Complete Checkouts

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var checkoutToken = "token";
var checkout = await service.CompleteAsync(checkoutToken);
```

### Get Checkouts

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var checkoutToken = "token";
var checkout = await service.GetAsync(checkoutToken);
```

### Updates Checkouts

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var checkoutToken = "token";
var checkout = await service.UpdateAsync(checkoutToken, new Checkout
{
    Email = "updated-email@nozzlegear.com"
});
```

### List Shipping Rates for Checkout

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var checkoutToken = "token";
var shippingRates = await service.ListShippingRatesAsync(checkoutToken);
```