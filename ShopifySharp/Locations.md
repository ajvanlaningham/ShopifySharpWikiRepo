## Locations

A Location represents a geographical location where your stores, headquarters, and/or pop-up shops exist. These locations can be used to track sales and to help Shopify configure the tax rates to charge when selling products.

### Listing locations

```cs
var service = new LocationService(myShopifyUrl, shopAccessToken);
var locations = await service.ListAsync();
```

### Getting a location

```cs
var service = new LocationService(myShopifyUrl, shopAccessToken);
var location = await service.GetAsync(locationId);
```