## Pages

A `Page` represents a web page on the merchant's Shopify storefront.

### Creating a page

```cs
var service = new PageService(myShopifyUrl, shopAccessToken);
var page = new Page()
{
    CreatedAt = DateTime.UtcNow,
    Title = "Burton Custom Freestlye 151",
    BodyHtml = "<strong>Good snowboard!</strong>",
};

page = await service.CreateAsync(page);
```

### Counting a page

```cs
var service = new PageService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync();
```

### Listing pages

```cs
var service = new PageService(myShopifyUrl, shopAccessToken);
var pages = await service.ListAsync();
```

### Retrieving a page

```cs
var service = new PageService(myShopifyUrl, shopAccessToken);
var page = await service.GetAsync(pageId);
```

### Updating a page

```cs
var service = new PageService(myShopifyUrl, shopAccessToken);
var page = await service.UpdateAsync(pageId, new Page()
{
    Title = "My new page title"
});
```

### Deleting a page

```c#
var service = new PageService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(pageId);
```