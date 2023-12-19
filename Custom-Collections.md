# Custom Collections

A custom collection is a grouping of products that a shop owner can create to make their shops easier to browse. A shop owner creates a custom collection and then selects the products that will go into it.

### Creating a custom collection

```cs
var service = new CustomCollectionService(myShopifyUrl, shopAccessToken);
var collection = await service.CreateAsync(new CustomCollection()
{
    Title = "My Custom Collection",
    Published = true,
    PublishedAt = DateTime.UtcNow,
    Image = new CustomCollectionImage()
    {
        Src = "https://placekitten.com/250/250"
    }
});
```

### Getting a custom collection

```cs
var service = new CustomCollectionService(myShopifyUrl, shopAccessToken);
var collection = await service.GetAsync(collectionId);
```

### Counting custom collections

```cs
var service = new CustomCollectionService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync();
```

### Listing custom collections

```cs
var service = new CustomCollectionService(myShopifyUrl, shopAccessToken);
var collections = await service.ListAsync();
```

### Updating a custom collection

```cs
var service = new CustomCollectionService(myShopifyUrl, shopAccessToken);
var collection = await service.UpdateAsync(collectionId, new Collection()
{
    Title = "My new collection title"
});
```

### Deleting a custom collection

```cs
var service = new CustomCollectionService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(collectionId);
```