## Draft Orders

You can use the DraftOrder resource to allow merchants to create orders on behalf of customers. This is useful for Shopify merchants who receive orders through outside channels and enables a wide range of use cases including the following:

-   Create new orders for sales made by phone, in person, via chat, or by other means. Credit card payments for these orders can subsequently be entered in the Shopify admin.
-   Send invoices to customers to pay with a secure checkout link.
-   Use custom items to represent additional costs or products that aren't displayed in a shop's inventory.
-   Re-create mistaken orders.
-   Sell products at discount or wholesale rates.
-   Take pre-orders.

### Listing Draft Orders

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
var draftOrders = await service.ListAsync();
```

### Counting Draft orders

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync();
```

### Getting a Draft Order

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
var draftOrder = await service.GetAsync(draftOrderId);
```

### Create a Draft Order

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
var draftOrder = await Service.CreateAsync(new DraftOrder()
{
    LineItems = new List<DraftLineItem>()
    {
        new DraftLineItem()
        {
            Title = "My custom line item",
            Price = 15.00m,
            Quantity = 1,
        }
    },
    Note = "Hello world!"
});
```

### Update a Draft Order

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
var original = await Service.GetAsync(originalOrderId);
original.Note = "My new note";

var updated = await Service.UpdateAsync(originalOrderId, original);
```

### Delete a Draft Order

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(orderId);
```

### Send a Draft Order invoice

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
var invoice = await service.SendInvoiceAsync(new DraftOrderInvoice()
{
    To = "customer@example.com",
    Subject = "Your order is ready to pay",
    CustomMessage = "Please pay!"
});
```

### Complete a Draft Order

```cs
var service = new DraftOrderService(myShopifyUrl, shopAccessToken);
bool paymentPending = false;
var draftOrder = await service.CompleteAsync(orderId, paymentPending);
```