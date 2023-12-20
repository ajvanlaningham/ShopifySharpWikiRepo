## Collects

A `Collect` is an object that connects a product to a custom collection.

### Creating a collect

```c#
var service = new CollectService(myShopifyUrl, shopAccessToken);
var collect = new Collect()
{
    CollectionId = collectionId,
    ProductId = productId
}

collect = await service.CreateAsync(collect);
```

### Retrieving a collect

```c#
var service = new CollectService(myShopifyUrl, shopAccessToken);
var collect = await service.GetAsync(collectId);
```

### Deleting a collect

```c#
var service = new CollectService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(collectId);
```

### Counting collects

```c#
var service = new CollectService(myShopifyUrl, shopAccessToken);
int collectCount = await service.CountAsync();

//Optionally filter the count to only those collects for a certain product or collection
int filteredCollectCount = await service.CountAsync(new CollectFilterOptions()
{
    ProductId = productId,
    CollectionId = collectionId
});
```

### Listing collects

```c#
var service = new CollectService(myShopifyUrl, shopAccessToken);
var collects = await service.ListAsync();

//Optionally filter the list to only those collects for a certain product or collection
var filteredCollects = await service.CountAsync(new CollectFilterOptions()
{
    ProductId = productId,
    CollectionId = collectionId
});
```

---