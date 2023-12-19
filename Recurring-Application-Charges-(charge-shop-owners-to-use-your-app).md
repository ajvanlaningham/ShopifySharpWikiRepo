## Recurring Application Charges (charge shop owners to use your app)

The Shopify billing API lets you create a recurring charge on a shop owner's account, letting them pay you for using your application. There are pros and cons to using the Shopify billing API versus a service like Stripe, BrainTree or PayPal.

I've put together a small guide called **_Shopify Billing 101: A Developer's Guide To Getting Paid For Your Apps_**,
and you can get for **free** by joining the mailing list for **_Mastering Shopify Development_** (a training course
for building Shopify apps with C# and ASP.NET).

[Just head over here to get your free guide to the Shopify billing API.](https://nozzlegear.com/landing/shopify-billing-101?ref=ShopifySharp)

Note that recurring charges are activated immediately after a user accepts them. At one time it was necessary to activate the charge after it was accepted, but Shopify has changed this behavior and it's no longer required or possible.

### Create a recurring charge

```c#
var service = new RecurringChargeService(myShopifyUrl, shopAccessToken);
var charge = new RecurringCharge()
{
    Name = "Lorem Ipsum Plan",
    Price = 12.34,
    Test = true, //Marks this charge as a test, meaning it won't charge the shop owner.
    TrialDays = 21
}

charge = await service.CreateAsync(charge);
```

### Retrieve a recurring charge

```c#
var service = new RecurringChargeService(myShopifyUrl, shopAccessToken);

var charge = await service.GetAsync(chargeId);
```

### Listing recurring charges

```c#
var service = new RecurringChargeService(myShopifyUrl, shopAccessToken);

IEnumerable<RecurringCharge> charges = await service.ListAsync();
```

### Deleting a charge

Charges cannot be deleted unless they've been activated. Shopify automatically deletes pending charges
after 48 hours pass without activation.

```c#
var service = new RecurringChargeService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(chargeId);
```

## One-time application charges

Just like with the above recurring charges, the Shopify billing API lets you create a one-time application
charge on the shop owner's account. One-time charges cannot be deleted.

### Create a one-time charge

```c#
var service = new ChargeService(myShopifyUrl, shopAccessToken);
var charge = new Charge()
{
    Name = "Lorem Ipsum Charge",
    Price = 12.34,
    Test = true, //Marks this charge as a test, meaning it won't charge the shop owner.
}

charge = await service.CreateAsync(charge);
```

### Retrieve a one-time charge

```c#
var service = new ChargeService(myShopifyUrl, shopAccessToken);

var charge = await service.GetAsync(chargeId);
```

### Listing one-time charges

```c#
var service = new ChargeService(myShopifyUrl, shopAccessToken);

IEnumerable<Charge> charges = await service.ListAsync();
```

### Activating a charge

Just like recurring charges, creating a one-time charge does not actually charge the shop owner. You need to
send them to the charge's `ConfirmationUrl`, have them accept the charge, then activate it.

```c#
var service = new ChargeService(myShopifyUrl, shopAccessToken);

await service.ActivateAsync(chargeId);
```

## Usage charges

Shopify's Usage Charges let you set a capped amount on a recurring application charge, and only charge for usage. For example, you can create a charge that's capped at $100.00 per month, and then charge e.g. $1.00 for every 1000 emails your user sends using your app.

To create a UsageCharge, you first need to create a RecurringCharge with a `CappedAmount` value and a `Terms` string. Your customers will see the terms when activating the recurring charge, so set it to something they can read like "\$1.00 per 1000 emails".

### Create a usage charge

```cs
var service = new UsageChargeService(myShopifyUrl, shopAccessToken);

string description = "Used 1000 emails";
double price = 1.00;

var usageCharge = await service.CreateAsync(recurringChargeId, description, price);
```

### Get a usage charge

```cs
var service = new UsageChargeService(myShopifyUrl, shopAccessToken);

var usageCharge = await service.GetAsync(recurringChargeId, usageChargeId);
```

### List usage charges

```cs
var service = new UsageChargeService(myShopifyUrl, shopAccessToken);

var usageCharges = await service.ListAsync(recurringChargeId);
```

