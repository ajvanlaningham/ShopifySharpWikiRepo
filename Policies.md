## Policies

Developers can get the list of policies that a merchant has configured for their store, such as their refund or privacy policies.

### Listing Policies

```cs
var service = new PolicyService(myShopifyUrl, shopAccessToken);
var policies = await service.ListAsync();
```