## Transactions

Transactions are created for every order that results in an exchange of money. All transactions are tied to a single order.

### Creating a full capture transaction

By omitting an `Amount` value, this transaction will capture the full amount.

**Note**: to create a `Capture` transaction, the order must have an `Authorization` transaction on it. However, an `Authorization` transaction can only be created at the time the order was created.

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var transaction = new Transaction()
{
    Kind = "capture"
};

await service.CreateAsync(orderId, transaction);
```

### Creating a partial capture transaction

This method will capture a specified amount on a previously authorized order.

**Note**: to create a `Capture` transaction, the order must have an `Authorization` transaction on it. However, an `Authorization` transaction can only be created at the time the order was created.

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var transaction = new Transaction()
{
    Kind = "capture",
    Amount = 5.00
};

await service.CreateAsync(orderId, transaction);
```

### Creating a refund transaction

This method will create a refund on a previously authorized order. Like the last two examples, you can either refund a partial amount by setting the `Amount` value, or refund the full amount by omitting that value.

**Note**: to create a `Refund` transaction, the order must have an `Authorization` transaction on it. However, an `Authorization` transaction can only be created at the time the order was created.

**Additionally**, it seems you can't create a `Refund` transaction for any order that was created via the API. (I can't find any documentation about this behavior. Let me know if this is wrong.)

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var transaction = new Transaction()
{
    Kind = "refund",
    Amount = 5.00
};

await service.CreateAsync(orderId, transaction);
```

### Creating a cancel transaction

This method is supposed to cancel a previously authorized order's payment. **However**, the Shopify API will throw an error whenever you try to do this. It may be that, like the refund transaction, you can't cancel an order that was created via the API. Again, there's no documentation for this behavior, let me know if you have any information.

That in mind, I'm including this example for posterity.

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var transaction = new Transaction()
{
    Kind = "void"
};

//Throws an error.
await service.CreateAsync(orderId, transaction);
```

### Getting a transaction

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var transaction = await service.GetAsync(orderId, transactionId);
```

### Counting transactions

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync(orderId);
```

### Listing transactions

```cs
var service = new TransactionService(myShopifyUrl, shopAccessToken);
var transactions = await service.ListAsync(orderId);

//Optionally filter the list to those after the given id
var transactions = await service.ListAsync(orderId, sinceId);
```

## Tender Transactions

Each tender transaction represents money passing between the merchant and a customer. A tender transaction with a positive amount represents a transaction where the customer paid money to the merchant. A negative amount represents a transaction where the merchant refunded money back to the customer. Tender transactions represent transactions that modify the shop's balance.

### Listing tender transactions

```cs
var service = new TenderTransactionService(myShopifyUrl, shopAccessToken);
var tenderTransactions = await service.ListAsync();

//Optionally filter the list to transactions processed after the specified date/time
var transactions = await service.ListAsync(new TenderTransactionListFilter
{
    ProcessedAtMin = DateTimeOffset.Now.AddHours(-1)
});
```