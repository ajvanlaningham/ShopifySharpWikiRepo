## Articles

Articles are objects representing a blog post. Each article belongs to a [Blog](#blogs).

### Creating an Article

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
var article = await service.CreateAsync(blogId, new Article()
{
    Title = "My new Article title",
    Author = "John Smith",
    Tags = "This Post, Has Been Tagged",
    BodyHtml = "<h1>Hello world!</h1>",
    Image = new ArticleImage()
    {
        Attachment = "R0lGODlhAQABAIAAAAAAAAAAACH5BAEAAAAALAAAAAABAAEAAAICRAEAOw==\n"
    }
});
```

### Getting an Article

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
var article = await service.GetAsync(blogId, articleId);
```

### Updating an Article

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
var article = await service.UpdateAsync(blogId, articleId, new Article()
{
    Title = "My new title"
});
```

### Listing Articles

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
var articles = await service.ListAsync(blogId);
```

### Counting Articles

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync(blogId);
```

### Deleting an Article

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(blogId, articleId);
```

### Listing all Article authors

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
IEnumerable<string> authors = await service.ListAuthorsAsync();
```

### Listing all Article tags

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
IEnumerable<string> tags = await service.ListTagsAsync();
```

### Listing all Article tags for a single Blog

```cs
var service = new ArticleService(myShopifyUrl, shopAccessToken);
IEnumerable<string> tags = await service.ListTagsForBlogAsync(blogId);
```