## Customers

### Creating a customer

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
var customer = new Customer()
{
    FirstName = "John",
    LastName = "Doe",
    Email = "john.doe@example.com",
    Addresses = new List<Address>()
    {
        new Address()
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
        }
    },
    VerifiedEmail = true,
    Note = "Test note about the customer.",
    State = "enabled"
};

customer = await service.CreateAsync(customer);
```

### Retrieving a customer

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
var customer = await service.GetAsync(customerId);
```

### Retrieving a customer with certain fields

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
var customer = await service.GetAsync(customerId, "first_name,last_name,email");

//Returns a customer with only FirstName, LastName and Email fields. All other fields are null.
```

### Updating a customer

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
var customer = await service.UpdateAsync(customerId, new Customer()
{
    Email = "test-update@example.com"
});
```

### Deleting a customer

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(customerId);
```

### Counting customers

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
int customerCount = await service.CountAsync();
```

### Listing customers

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
IEnumerable<Customer> customers = await Service.ListAsync();
```

### Listing orders for a customer

```c#
var service =  new CustomerService(myShopifyUrl, shopAccessToken);
IEnumerable<Order> orders = await service.ListOrdersForCustomerAsync(customerId);
```

### Searching customers

Use a `CustomerSearchListFilter` to perform searches for customers. There is a noticeable 3-30 second delay between creating a new customer and Shopify indexing it for a search.

```c#
var service = new CustomerService(myShopifyUrl, shopAccessToken); 
var filter = new CustomerSearchListFilter
{
  //Searches for a customer from the United States with a name like 'Jane'.
  Query = "Jane country:United States"
};
IEnumerable<Customer> customers = await Service.SearchAsync(filter);
```