## Order Risks

The Order risk assessment is used to indicate to a merchant the fraud checks that have been done on an order.

### Create an Order Risk

```cs
var service = new OrderRiskService(myShopifyUrl, shopAccessToken);
var risk = await service.CreateAsync(orderId, new OrderRisk()
{
    Message = "This looks risk!",
    Score = (decimal)0.85,
    Recommendation = "cancel",
    Source = "External",
    CauseCancel = false,
    Display = true,
});
```

### Get an Order Risk

```cs
var service = new OrderRiskService(myShopifyUrl, shopAccessToken);
var risk = await service.GetAsync(orderId, riskId);
```

### Update an Order Risk

```cs
var service = new OrderRiskService(myShopifyUrl, shopAccessToken);
var risk = await service.UpdateAsync(orderId, riskId, new Risk()
{
    Message = "An updated risk message"
});
```

### List Order Risks

```cs
var service = new OrderRiskService(myShopifyUrl, shopAccessToken);
var risks = await service.ListAsync(orderId);
```

### Delete an Order Risk

```cs
var service = new OrderRiskService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(orderId, riskId);
```
