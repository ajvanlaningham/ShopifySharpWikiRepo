## Blogs

In addition to an online storefront, Shopify shops come with a built-in blogging engine, allowing a shop to have one or more blogs. **This service is for interacting with blogs themselves, not [blog posts](#articles)**.

### Creating a Blogs

```cs
var service = new BlogService(myShopifyUrl, shopAccessToken);
var blog = await service.CreateAsync(new Blog()
{
    Title = "My new blog"
});
```

### Getting a Blog

```cs
var service = new BlogService(myShopifyUrl, shopAccessToken);
var blog = await service.GetAsync(blogId);
```

### Updating a Blog

```cs
var service = new BlogService(myShopifyUrl, shopAccessToken);
var blog = await service.UpdateAsync(blogId, new Blog()
{
    Comments = "moderate"
});
```

### Listing Blogs

```cs
var service = new BlogService(myShopifyUrl, shopAccessToken);
var blogs = await service.ListAsync();
```

### Counting Blogs

```cs
var service = new BlogService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync();
```

### Deleting a Blog

```cs
var service = new BlogService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(blogId);
```