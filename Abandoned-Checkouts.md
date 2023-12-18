## Abandoned Checkouts

This is used to return abandoned checkouts. A checkout is considered abandoned when a customer has entered their billing & shipping info, but has yet to complete the purchase.

### Listing Abandoned Checkouts

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var checkouts = await service.ListAsync();
```

### Count Abandoned Checkouts

```cs
var service = new CheckoutService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync();
```