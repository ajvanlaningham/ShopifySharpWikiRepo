## Shops

### Retrieving shop information

```c#
var service = new ShopService(myShopifyUrl, shopAccessToken);

var shop = await service.GetAsync();
```

### Uninstalling your app

In cases where user intervention is not required, you can send a request to a Shopify shop to force it to uninstall your application. After sending this request, your shop access token will be immediately revoked and invalidated.

Uninstalling an application is an irreversible operation. Be entirely sure that you no longer need to make API calls for the shop in which the application has been installed.

Uninstalling an application also performs various cleanup tasks within Shopify. Registered Webhooks, ScriptTags and App Links will be destroyed as part of this operation. Also if an application is uninstalled during key rotation, both the old and new Access Tokens will be rendered useless.

```cs
var service = new ShopService(myShopifyUrl, shopAccessToken);

var shop = await service.UninstallAppAsync()
```
