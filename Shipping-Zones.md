## Shipping Zones

Developers can get the list of shipping zones, their countries, provinces, and shipping rates.

### Listing Shipping Zones

```cs
var service = new ShippingZoneService(myShopifyUrl, shopAccessToken);
var shippingZones = await service.ListAsync();
```