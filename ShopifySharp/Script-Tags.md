## Script Tags

Script tags let you add remote javascript tags that are loaded into the pages of a shop's storefront, letting you
dynamically change the functionality of their shop without manually editing their store's template.

### Creating a script tag

```c#
var service = new ScriptTagService(myShopifyUrl, shopAccessToken);
var tag = new ScriptTag()
{
    Event = "onload",
    Src  = "https://example.com/my-javascript-file.js",
    DisplayScope = 'all'
}

tag = await service.CreateAsync(tag);
```

### Retrieving a script tag

```c#
var service = new ScriptTagService(myShopifyUrl, shopAccessToken);
var tag = await service.GetAsync(tagId);
```

### Updating a script tag

```c#
var service = new ScriptTagService(myShopifyUrl, shopAccessToken);
var tag = await service.UpdateAsync(tagId, new ScriptTag()
{
    Src = "https://example.com/my-new-javascript-file.js";
});
```

### Deleting a script tag

```c#
var service = new ScriptTagService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(tagId);
```

### Counting script tags

```c#
var service = new ScriptTagService(myShopifyUrl, shopAccessToken);
int tagCount = await service.CountAsync();

//Optionally filter the count to only those tags with a specific Src
int filteredTagCount = await service.CountAsync("https://example.com/my-filtered-url.js");
```

### Listing script tags

```c#
var service = new ScriptTagService(myShopifyUrl, shopAccessToken);
var tags = await service.ListAsync();

//Optionally filter the list to only those tags with a specific Src
var filteredTags = await service.ListAsync(new ScriptTagListOptions() {
    Src = FilteredSrc
});
```
