## Orders

### Creating an order

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);
var order = new Order()
{
    CreatedAt = DateTime.UtcNow,
    BillingAddress = new Address()
    {
        Address1 = "123 4th Street",
        City = "Minneapolis",
        Province = "Minnesota",
        ProvinceCode = "MN",
        Zip = "55401",
        Phone = "555-555-5555",
        FirstName = "John",
        LastName = "Doe",
        Company = "Tomorrow Corporation",
        Country = "United States",
        CountryCode = "US",
        Default = true,
    },
    LineItems = new List<LineItem>()
    {
        new LineItem()
        {
            Name = "Test Line Item",
            Title = "Test Line Item Title"
        }
    },
    FinancialStatus = "paid",
    TotalPrice = 5.00,
    Email = Guid.NewGuid().ToString() + "@example.com",
    Note = "Test note about the customer.",
};

order = await service.CreateAsync(order);
```

### Retrieving an order

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);
var order = await service.GetAsync(orderId);
```

### Updating an order

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);
var order = await service.UpdateAsync(orderId, new Order()
{
    Notes = "test notes."
});
```

### Deleting an order

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(orderId);
```

### Counting orders

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);
int orderCount = await service.CountAsync();
```

### Listing orders

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);
IEnumerable<Order> orders = await service.ListAsync();
```

### Close an order

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);

await service.CloseAsync(orderId);
```

### Reopen a closed order

```c#
var service = new OrderService(myShopifyUrl, shopAccessToken);

await service.OpenAsync(orderId);
```

### Cancel an order

```cs
var service = new OrderService(myShopifyUrl, shopAccessToken);

await service.CancelAsync(orderId);
```
