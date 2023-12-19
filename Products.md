## Products

### Creating a product

```c#
var service = new ProductService(myShopifyUrl, shopAccessToken);
var product = new Product()
{
    Title = "Burton Custom Freestlye 151",
    Vendor = "Burton",
    BodyHtml = "<strong>Good snowboard!</strong>",
    ProductType = "Snowboard",
    Images = new List<ProductImage>
    {
        new ProductImage
        {
            Attachment = "R0lGODlhAQABAIAAAAAAAAAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw=="
        }
    },
};

product = await service.CreateAsync(product);

//By default, creating a product will publish it. To create an unpublished product:+1:
product = await service.CreateAsync(product, new ProductCreateOptions() { Published = false });

```

### Retrieving a product

```c#
var service = new ProductService(myShopifyUrl, shopAccessToken);
var product = await service.GetAsync(productId);
```

### Updating a product

```c#
var service = new ProductService(myShopifyUrl, shopAccessToken);
var product = await service.UpdateAsync(productId, new Product()
{
    Title = "New product title"
});
```

### Deleting a product

```c#
var service = new ProductService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(productId);
```

### Counting products

```c#
var service = new ProductService(myShopifyUrl, shopAccessToken);
int productCount = await service.CountAsync();
```

### Listing products

```c#
var service = new ProductService(myShopifyUrl, shopAccessToken);
IEnumerable<Product> products = await service.ListAsync();

//Optionally filter the results
var filter = new ProductFilterOptions()
{
    Ids = new[]
    {
        productId1,
        productId2,
        productId3
    }
};
products = await service.ListAsync(filter);
```

### Publishing a product

```cs
var service = new ProductService(myShopifyUrl, shopAccessToken);
var product = await service.PublishAsync(productId);
```

### Unpublishing a product

```cs
var service = new ProductService(myShopifyUrl, shopAccessToken);
var product = await service.UnpublishAsync(productId);
```