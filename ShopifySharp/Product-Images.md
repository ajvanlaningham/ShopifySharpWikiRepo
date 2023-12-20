## Product Images

Product Images represent the various different images for a product. All product images are tied to an owner product, and therefore you'll need to pass that product's id to each product image method.

### Creating a product image

```cs
var service = new ProductImageService(myShopifyUrl, shopAccessToken);
var image = await service.CreateAsync(productId, new ProductImage()
{
    Metafields = new List<MetaField>()
    {
        new MetaField()
        {
            Key = "alt",
            Value = "new alt tag content",
            ValueType = "string",
            Namespace = "tags"
        }
    },
    Src = "https://placekitten.com/200/300"
});
```

### Getting a product image

```cs
var service = new ProductImageService(myShopifyUrl, shopAccessToken);
var image = await service.GetAsync(productId, imageId);
```

### Counting product images

```cs
var service = new ProductImageService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync(productId);
```

### Listing product images

```cs
var service = new ProductImageService(myShopifyUrl, shopAccessToken);
var images = await service.ListAsync(productId);
```

### Updating a product image

```cs
var service = new ProductImageService(myShopifyUrl, shopAccessToken);
var image = await service.UpdateAsync(productId, imageId, new Image()
{
    Position = 2
});
```

### Deleting a product image

```cs
var service = new ProductImageService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(productId, imageId);
```