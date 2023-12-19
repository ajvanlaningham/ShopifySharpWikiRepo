## Gift Cards

Developers can create a gift card with the `GiftCardService`.

**Gift Cards require a Shopify Plus subscription.**

### Listing Gift Cards

```cs
var service = new GiftCardService(myShopifyUrl, shopAccessToken);
var giftCards = await service.ListAsync();
```

### Creating a Gift Card

```cs
var service = new GiftCardService(myShopifyUrl, shopAccessToken);
var giftCard = await service.CreateAsync(new GiftCard()
{
    InitialValue = 100,
    Code = "abc-bcd-efg"
});
```

### Getting a Gift Card

```cs
var service = new GiftCardService(myShopifyUrl, shopAccessToken);
var giftCard = await service.GetAsync(giftCardId):
```

### Disabling a Gift Card

Gift Cards can be disabled via that API, which makes them inactive and unusable until reenabled.

```cs
var service = new GiftCardService(myShopifyUrl, shopAccessToken);

await service.DisableAsync(discountId);
```

### Counting a Gift Cards

```c#
var service =  new GiftCardService(myShopifyUrl, shopAccessToken);
int giftCardCount = await service.CountAsync();
```

### Searching a Gift Cards

```c#
var service =  new GiftCardService(myShopifyUrl, shopAccessToken);
IEnumerable<GiftCard> giftCards = await Service.SearchAsync("code: abc-bcd-efg");
```

## Gift Card Adjustments

Developers can create adjustments on existing gift cards with the `GiftCardAdjustmentService`.

**Gift Cards require a Shopify Plus subscription and also the Gift Card Adjustment endpoint needs to be enabled on your store, contact Shopify plus support for more info.**

### Listing Gift Card Adjustments

```cs
var service = new GiftCardAdjustmentService(myShopifyUrl, shopAccessToken);
var giftCardAdjustments = await service.ListAsync(giftCardId);
```

### Creating a Gift Card Adjustment

```cs
var service = new GiftCardAdjustmentService(myShopifyUrl, shopAccessToken);
var giftCard = await service.CreateAsync(giftCardId, new GiftCardAdjustment()
{
    Amount = -1.00,
});
```

### Getting a Gift Card Adjustment

```cs
var service = new GiftCardAdjustmentService(myShopifyUrl, shopAccessToken);
var giftCardAdjustment = await service.GetAsync(giftCardId, adjustmentId):
```
