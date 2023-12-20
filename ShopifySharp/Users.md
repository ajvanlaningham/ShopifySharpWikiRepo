## Users

Developers can retrieve users with the `UserService`.

**The Users API requires a Shopify Plus subscription.**

### Listing Users

```cs
var service = new UserService(myShopifyUrl, shopAccessToken);
var users = await service.ListAsync();
```

### Getting a User

```cs
var service = new UserService(myShopifyUrl, shopAccessToken);
var user = await service.GetAsync(userId):
```