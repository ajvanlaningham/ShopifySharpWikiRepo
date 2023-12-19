## Price Rules

The Price Rules API allows you to dynamically create discounts with multiple conditions that can be applied at checkout to cart items or shipping lines via a discount code. Price rules can be created for a fixed value discount, a percentage discount, or a shipping line discount. You can also specify the dates for which the price rule is valid, the number of times the price rule can be applied, and to which products, collections, variants, customer groups and even shipping countries the price rule can be applied.

### Creating a Price Rule

```cs
var service = new PriceRuleService(myShopifyUrl, shopAccessToken);
var priceRule = await service.CreateAsync(new PriceRule()
{
    Title = "My price rule",
    ValueType = "percentage",
    TargetType = "line_item",
    TargetSelection = "all",
    AllocationMethod = "across",
    Value = -10.0m,
    CustomerSelection = "all",
    OncePerCustomer = false,
    PrerequisiteSubtotalRange = new PrerequisiteValueRange()
    {
        GreaterThanOrEqualTo = 40m
    },
    StartsAt = new DateTimeOffset(DateTime.Now)
});
```

### Updating a Price Rule

```cs
var service = new PriceRuleService(myShopifyUrl, shopAccessToken);
var updatedRule = await service.UpdateAsync(ruleId, new PriceRule()
{
    Value = -15.0m
});
```

### Getting a Price Rule

```cs
var service = new PriceRuleService(myShopifyUrl, shopAccessToken);
var priceRule = await service.GetAsync(ruleId);
```

### Listing Price Rules

```cs
var service = new PriceRuleService(myShopifyUrl, shopAccessToken);
var priceRules = await service.ListAsync();
```

### Deleting a Price Rule

```cs
var service = new PriceRuleService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(ruleId);
```