## Discounts

Developers can create a discount code with the `DiscountService`. A merchant's customers can enter the discount code during the checkout process to redeem percentage-based, fixed amount, or free shipping discounts on a specific product, collection or order.

**Discounts require a Shopify Plus subscription.**

### Creating a Discount

```cs
var service = new DiscountService(myShopifyUrl, shopAccessToken);
var discount = await service.CreateAsync(new Discount()
{
    DiscountType = "fixed_amount",
    Value = "10.00",
    DiscountCode = "AuntieDot",
    MinimumOrderAmount = "40.00",
});
```

### Getting a Discount

```cs
var service = new DiscountService(myShopifyUrl, shopAccessToken);
var discount = await service.GetAsync(discountId):
```

### Listing Discounts

```cs
var service = new DiscountService(myShopifyUrl, shopAccessToken);
var discounts = await service.ListAsync();
```

### Deleting a Discount

```cs
var service = new DiscountService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(discountId);
```

### Disabling a Discount

Discount codes can be disabled via that API, which makes them inactive and unusable until reenabled.

```cs
var service = new DiscountService(myShopifyUrl, shopAccessToken);

await service.DisableAsync(discountId);
```

### Enabling a Discount

Once disabled, a discount cannot be used by any customer until it's enabled.

```cs
var service = new DiscountService(myShopifyUrl, shopAccessToken);

await service.EnableAsync(discountId);
```
