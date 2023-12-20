## Redirects

A `Redirect` lets you create URL redirects on a Shopify store. When a store visitor navigates to a redirect's `Path`, they'll be redirected to the redirect's `Target`.

### Creating a redirect

```c#
var service = new RedirectService(myShopifyUrl, shopAccessToken);
var redirect = new Redirect()
{
    Path = "/ipod",
    Target  = "https://apple.com/ipod"
}

redirect = await service.CreateAsync(redirect);
```

### Retrieving a redirect

```c#
var service = new RedirectService(myShopifyUrl, shopAccessToken);
var redirect = await service.GetAsync(redirectId);
```

### Updating a redirect

```c#
var service = new RedirectService(myShopifyUrl, shopAccessToken);
var redirect = await service.UpdateAsync(redirectId, new Redirect()
{
    Target = "https://apple.com/ipad",
    Path = "/ipad"
});
```

### Deleting a redirect

```c#
var service = new RedirectService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(redirectId);
```

### Counting redirects

```c#
var service = new RedirectService(myShopifyUrl, shopAccessToken);
int redirectCount = await service.CountAsync();

//Optionally filter the count to only those redirects with a specific path or target
int filteredRedirectCount = await service.CountAsync(path: "/ipod", target: "https://apple.com/ipod/");
```

### Listing redirects

```c#
var service = new RedirectService(myShopifyUrl, shopAccessToken);
var redirects = await service.ListAsync();

//Optionally filter the list to only those redirects with a specific path or target
var filteredRedirects = await service.ListAsync(new RedirectListOptions() {
    Path = "/ipod",
    Target = "https://apple.com/ipod"
});
```