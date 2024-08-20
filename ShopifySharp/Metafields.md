## Metafields

### Creating a metafield

```cs
var service = new MetaFieldService(myShopifyUrl, shopAccessToken);
var metafield = new MetaField()
{
    Namespace = "myNamespace",
    Key = "myKey",
    Value = "5",
    Type = "number_integer",
    Description = "This is a test meta field. It is an integer value."
};

//Create a new metafield on a product
metafield = await service.CreateAsync(metafield, productId, "products");
```

### Counting metafields

```cs
var service = new MetaFieldService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync(productId, "products");
```

### Listing metafields

```cs
var service = new MetaFieldService(myShopifyUrl, shopAccessToken);
var metafields = await service.ListAsync(productId, "products");
```

### Getting a metafield

```cs
var service = new MetaFieldService(myShopifyUrl, shopAccessToken);
var metafield = await service.GetAsync(metafieldId);
```

### Updating a metafield

```cs
var service = new MetaFieldService(myShopifyUrl, shopAccessToken);
var metafield = await service.UpdateAsync(metafieldId, new MetaField()
{
    Value = "45"
});
```

### Deleting a metafield

```cs
var service = new MetaFieldService(myShopifyUrl, shopAccessToken);
await service.DeleteAsync(metafieldId);
```
