## Access Scopes

The Access Scope API allows you to retrieve the permissions that a merchant has granted to an app, such as `read_orders` and `write_products`. The list of access scopes is retrieved based on the access token used for the request, and only returns those scopes associated with the token.

### List Access Scopes

```cs
var service = new AccessScopeService(myShopifyUrl, shopAccessToken);
var scopes = await service.ListAsync();
```
