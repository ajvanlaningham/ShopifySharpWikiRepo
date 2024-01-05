# ShopPlan

### GetShopPlanAsync

This method uses Shopify's GraphQL API to get the shop's subscription plan.

```var service = new ShopPlanService(shopDomain, accessToken);

var shopPlan = await service.GetShopPlanAsync();```

### IsPartnerDevelopmentShopAsync

This method uses Shopify's GraphQL API to check if the shop is a development shop. Returns true if `shop.plan.partnerDevelopment` is true.

```var service = new ShopPlanService(shopDomain, accessToken);

var isPartnerDevelopmentShop = await service.IsPartnerDevelopmentShopAsync();```