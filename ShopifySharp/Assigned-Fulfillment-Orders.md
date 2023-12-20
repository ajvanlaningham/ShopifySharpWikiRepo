## Assigned Fulfillment Orders

The AssignedFulfillmentOrder resource allows you to retrieve all the fulfillment orders that are assigned to an app at the shop level.

### Listing assigned fulfillment orders

Retrieves a list of fulfillment orders on a shop for a specific app.

```c#
var service = new AssignedFulfillmentOrderService(myShopifyUrl, shopAccessToken);

//Optionally filter the list to only those assigned fulfillments with a specific status
var filterStatus = new AssignedFulfillmentOrderFilter()
{
    AssignmentStatus = "fulfillment_requested"
});

var assignedFulfillments = await service.ListAsync(filterStatus);
```

---

## Cancellation Requests

The CancellationRequest resource represents a cancellation request made by the merchant or 
an order management app to a fulfillment service for a fulfillment order.

### Create A Cancellation Request

Send a cancellation request to the fulfillment service of a fulfillment order.

```c#
var service = new CancellationRequestService(myShopifyUrl, shopAccessToken);
var fulfillmentOrder = await service.CreateAsync(fulfillmentOrderId, "The customer changed his mind.");
```

### Accept A Cancellation Request

Accept a cancellation request sent to a fulfillment service for a fulfillment order.

```c#
var service = new CancellationRequestService(myShopifyUrl, shopAccessToken);
var fulfillmentOrder = await service.AcceptAsync(fulfillmentOrderId, "We had not started any processing yet.");
```

### Reject A Cancellation Request

Reject a cancellation request sent to a fulfillment service for a fulfillment order.

```c#
var service = new CancellationRequestService(myShopifyUrl, shopAccessToken);
var fulfillmentOrder = await service.AcceptAsync(fulfillmentOrderId, "We have already sent the shipment out.");
```

---

## Fulfillment Events

The FulfillmentEvent resource represents tracking events that belong to a fulfillment of one or more items in an order.

### Creates a fulfillment event

Creates a new FulfillmentEvent on the fulfillment.

```c#
var service = new FulfillmentEventService(myShopifyUrl, shopAccessToken);
var fulfillmentEvent = new FulfillmentEvent()
{
    OrderId = 1234532,
    FulfillmentId = 156185165,
    Status = "confirmed"
};

fulfillmentEvent = await service.CreateAsync(orderId, fulfillmentId, fulfillmentEvent);
```

### List fulfillment events

Retrieves a list of fulfillment events for a specific fulfillment

```c#
var service = new FulfillmentEventService(myShopifyUrl, shopAccessToken);
var fulfillmentEvents = await service.ListAsync(orderId, fulfillmentId);
```

### Get a Fulfillment Event

Retrieves a specific fulfillment event

```c#
var service = new FulfillmentEventService(myShopifyUrl, shopAccessToken);
var fulfillmentEvent = await service.GetAsync(orderId, fulfillmentId, fulfillmentEventId);
```

### Delete A Fulfillment Event

```cs
var service = new FulfillmentEventService(myShopifyUrl, shopAccessToken);
await service.DeleteAsync(orderId, fulfillmentId, fulfillmentEventId);
```

--

## Fulfillment Orders

The FulfillmentOrder resource represents either an item or a group of items in an order that are to 
be fulfilled from the same location. There can be more than one fulfillment order for an order at a given location.

> **TODO**
> - [X] Cancel a fulfillment order
> - [X] Mark a fulfillment order as incomplete
> - [ ] Move a fulfillment order to a new location
> - [ ] Mark the fulfillment order as open
> - [ ] Reschedule the fulfill_at time of a scheduled fulfillment order
> - [X] Retrieve a specific fulfillment order

### List Fulfillment Orders

Retrieves a list of fulfillment orders for a specific order

```c#
var service = new FulfillmentOrderService(myShopifyUrl, shopAccessToken);
var fulfillmentOrders = await service.ListAsync(orderId);
```

---

## Fulfillment Requests

The FulfillmentRequest resource represents a fulfillment request made by the merchant to a 
fulfillment service for a fulfillment order.

### Create A Fulfillment Request

Sends a fulfillment request to the fulfillment service of a fulfillment order

```c#
var service = new FulfillmentRequestService(myShopifyUrl, shopAccessToken);

// Optionally, you can request only specific item to fulfilled.
var fulfillmentRequest = new FulfillmentRequest()
{
    FulfillmentRequestOrderLineItems = new List<FulfillmentRequestOrderLineItems>(){}
};
var fulfillmentOrder = await service.CreateAsync(fulfillmentOrderId, fulfillmentRequest);
```

### Accept A Fulfillment Request

Accepts a fulfillment request sent to a fulfillment service for a fulfillment order

```c#
var service = new FulfillmentRequestService(myShopifyUrl, shopAccessToken);
var fulfillmentOrder = await service.AcceptAsync(fulfillmentOrderId, "Your order will be filled shortly.");
```

### Reject A Fulfillment Request

Reject a fulfillment request sent to a fulfillment service for a fulfillment order

```c#
var service = new FulfillmentRequestService(myShopifyUrl, shopAccessToken);
var fulfillmentOrder = await service.AcceptAsync(fulfillmentOrderId, "Fulfillment services have been suspended for this store.");
```

---

## Fulfillment Services

A Fulfillment Service is a third party warehouse that prepares and ships orders on behalf of the store owner. 
Fulfillment services charge a fee to package and ship items and update product inventory levels. 
Some well known fulfillment services with Shopify integrations include: Amazon, Shipwire, and Rakuten. 
When an app registers a new FulfillmentService on a store, Shopify automatically creates a Location 
that's associated to that fulfillment service.

### Create a Fulfillment Service

```c#
var service = new FulfillmentServiceService(myShopifyUrl, shopAccessToken);
var fulfillmentService = await service.CreateAsync(new FulfillmentServiceEntity()
{
    Name = "Your Company Name", 
    CallbackUrl = "http://yourcompany.com", 
    InventoryManagement = true,
    TrackingSupport = true,
    FulfillmentOrdersOptIn = true,
    RequiresShippingMethod = true, 
    Format = "json"
});
```

### List Fulfillment Services

Retrieves a list of fulfillment orders for a specific order

```c#
var service = new FulfillmentServiceService(myShopifyUrl, shopAccessToken);
// Optional Filter
var filter = new FulfillmentServiceListFilter(){ Scope = "all"};
var fulfillmentServices = await service.ListAsync(filter);
```

### Get a Fulfillment Service

Retrieves a single Fulfillment Service

```c#
var service = new FulfillmentServiceService(myShopifyUrl, shopAccessToken);
// Optional Filter
var fields = "id,name,email";
var fulfillmentService = await service.GetAsync(fulfillmentServiceId, fields);
```

### Modify a Fulfillment Service

Update a Fulfillment Service. Not all fields are updatable

```c#
var service = new FulfillmentServiceService(myShopifyUrl, shopAccessToken);
var fulfillmentService = await service.UpdateAsync(fulfillmentServiceId, fulfillmentServiceEntity);
```

### Delete a Fulfillment Service

```c#
var service = new FulfillmentServiceService(myShopifyUrl, shopAccessToken);
var fulfillmentService = await service.DeleteAsync(fulfillmentServiceId);
```

---