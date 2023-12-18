## Application Credits

Shopify's Application Credit API lets you offer credits for payments your app customers have made via the Application Charge, Recurring Application Charge, and Usage Charge APIs.

The total amount of all Application Credits created by an application must not exceed:

1. Total amount paid to the application by the shop owner in the last 30 days.
2. Total amount of pending receivables in the partner account associated with the application.

Additionally, Application Credits cannot be used by private applications.

### Creating an Application Credit

```cs
var service = new ApplicationCreditService(myShopifyUrl, shopAccessToken);
var credit = await service.CreateAsync(new ApplicationCredit()
{
    Description = "Refund for Foo",
    Amount = 10.00m
});
```

### Getting an Application Credit

```cs
var service = new ApplicationCreditService(myShopifyUrl, shopAccessToken);
var charge = await service.GetAsync(creditId);
```

### Listing Application Credits

```cs
var service = new ApplicationCreditService(myShopifyUrl, shopAccessToken);
var charges = await service.ListAsync();
```