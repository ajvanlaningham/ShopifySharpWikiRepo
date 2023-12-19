## Smart Collections

A smart collection is a grouping of products defined by simple rules set by shop owners. A shop owner creates a smart collection and then sets the rules that determine which products go in them. Shopify automatically changes the contents of smart collections based on their rules.

### Creating a Smart Collection

```cs
var service = new SmartCollectionService(myShopifyUrl, shopAccessToken);
var smartCollection = await service.CreateAsync(new SmartCollection()
{
   Title = "My Smart Collection",
   Handle = "my-url-slug",
   BodyHtml = "\<h1\>Hello world!\</h1\>",
   Image = new SmartCollectionImage()
   {
       // Base-64 image attachment
       Attachment = "R0lGODlhAQABAIAAAAAAAAAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==\n"
   }
});
```

### Updating a Smart Collection

```cs
var service = new SmartCollectionService(myShopifyUrl, shopAccessToken);
var smartCollection = await service.UpdateAsync(smartCollectionId, new SmartCollection()
{
    Title = "My updated title"
});
```

### Getting a Smart Collection

```cs
var service = new SmartCollectionService(myShopifyUrl, shopAccessToken);
var smartCollection = await service.GetAsync(smartCollectionId);
```

### Counting Smart Collections

```cs
var service = new SmartCollectionService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync();
```

### Listing Smart Collections

```cs
var service = new SmartCollectionService(myShopifyUrl, shopAccessToken);
var smartCollections = await service.ListAsync();
```

### Deleting a Smart Collection

```cs
var service = new SmartCollectionService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(smartCollectionId);
```