## Collections

API version 2020-01 introduces the new "Collections" endpoint, which can be used to get the base details and list of products associated with either a [Custom Collection](#custom-collections) or [Smart Collection](#smart-collections). 

This endpoint **cannot** be used to manipulate the products, collects, custom collections or smart collections. You must use the entity's respective ShopifySharp service to do that (i.e. `CollectService`, `ProductService`, `CustomCollectionService` and `SmartCollectionService`).

### Getting a Collection

```cs
var service = new CollectionService(myShopifyUrl, shopAccessToken);
var collection = await service.GetAsync(collectionId);
```

### Listing products belonging to a Collection

```cs
var service = new CollectionService(myShopifyUrl, shopAccessToken);
var products = await service.ListAsync(collectionId);
```