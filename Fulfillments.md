## Fulfillments

> **NOTE**: Shopify has changed how fulfillments are done in API version **2022-07 and above**. This takes affect in [ShopifySharp versions **5.19.0 and above**](#API-support). If you're using these versions of ShopifySharp, you should use fulfillment orders to create fulfillments, rather than the `FulfillmentService`. 
> 
> [Follow the example code in this issue](https://github.com/nozzlegear/ShopifySharp/issues/828) until our fulfillment documentation is updated.

A fulfillment represents a shipment of one or more items in an order. All fulfillments are tied to a single order.

### Creating a fulfillment for all fulfillment orders in Order

This will completely fulfill all of the fulfillment orders in the order.

```c#
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
var fulfillmentShipping = new FulfillmentShipping()
{
    Message = "Items will be shipped now.",
    NotifyCustomer = true,
    TrackingInfo = new TrackingInfo()
    {
        Number = "123456789",
        Url = "https://example.com/123456789",
        Company = "Jack Black's Pack, Stack and Track"
    },
    FulfillmentRequestOrderLineItems = []
};

fulfillment = await service.CreateAsync(fulfillmentShipping);
```

### Creating a fulfillment for single fulfillment order in order

This will fulfill all line items of the specified fulfillment orders.

```cs
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
var fulfillmentShipping = new FulfillmentShipping()
{
    Message = "Items will be shipped now.",
    NotifyCustomer = true,
    TrackingInfo = new TrackingInfo()
    {
        Number = "123456789",
        Url = "https://example.com/123456789",
        Company = "Jack Black's Pack, Stack and Track"
    },
    FulfillmentRequestOrderLineItems = new List<LineItemsByFulfillmentOrder>()
    {
        new LineItemsByFulfillmentOrder() 
        {
            FulfillmentOrderId = 1,
            FulfillmentRequestOrderLineItems = []
        }
    }
};

fulfillment = await service.CreateAsync(fulfillmentShipping);
```

### Retrieving a fulfillment

```c#
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
var fulfillment = await service.GetAsync(orderId, fulfillmentId);
```

### Updating a fulfillment

```cs
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
var fulfillment = await service.UpdateAsync(orderId, fulfillmentId, new Fulfillment()
{
    TrackingCompany = "John Doe's Tracking Company"
});
```

### Counting fulfillments

```c#
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
int fulfillmentCount = await service.CountAsync(orderId);
```

### Listing fulfillments

```c#
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
var fulfillments = await service.ListAsync(orderId);
```

### Cancelling a fulfillment

Fulfillments can only be cancelled if their `Status` is `pending`.

```cs
var service = new FulfillmentService(myShopifyUrl, shopAccessToken);
await service.CancelAsync(fulfillmentId)
```

---
