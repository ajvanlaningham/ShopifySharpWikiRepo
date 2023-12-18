## Assets

The `AssetService` lets you create, update and delete a store theme's asset files. Unlike other API services in ShopifySharp, the `AssetService` has a single `.CreateOrUpdateAsync` method due to the way Shopify's API handles assets. If an asset has a unique `Key` value, it will be created. If not, it will be updated. You can copy an asset by setting the new asset's `SourceKey` to the target's `Key` value.

Shopify asset's do not have an id, but rather a key string; they're also organized into type 'buckets'. For a liquid template, it's full key would be `templates/liquid.index`; for an image, its key would be `assets/my-image.png`.

Finally, all assets are tied to a specific theme, and you need that theme's id to interact with assets. You can use the [`ThemeService`](#themes) to get a list of the shop's themes, or the `ShopService` to get the currently active theme's id.

### Creating an asset

```cs
var service = new AssetService(myShopifyUrl, shopAccessToken);
var asset = new Asset()
{
    ContentType = "text/x-liquid",
    Key = "templates/test.liquid",
    Value  = "<h1>Hello, world!</h1>"
}

//Note: Creating an asset does not return it's 'Value' property.
//You must specifically refresh it with service.GetAsync
asset = await service.CreateAsync(themeId, asset);
```

### Retrieving an asset

```cs
var service = new AssetService(myShopifyUrl, shopAccessToken);
var key = "templates/index.liquid";

var asset = await service.GetAsync(themeId, key);
```

### Listing assets

```cs
var service = new AssetService(myShopifyUrl, shopAccessToken);

var assets = await service.ListAsync(themeId);
```

### Updating assets

```cs
var service = new AssetService(myShopifyUrl, shopAccessToken);

//Note: Updating an asset does not return it's 'Value' property.
//You must specifically refresh it with service.GetAsync
var asset = await service.UpdateAsync(themeId, assetId, new Asset()
{
    Value = "<h1>Hello, world! I've been updated.</h1>";
});
```

### Copying an asset

You can create a new asset by copying an already existing one. Just set the new asset's `SourceKey` property to
match the target's `Key` property.

```cs
var service = new AssetService(myShopifyUrl, shopAccessToken);
var asset = new Asset()
{
    Key = "templates/test.liquid",
    SourceKey = originalAsset.Key
};

//Note: Creating an asset does not return it's 'Value' property.
//You must specifically refresh it with service.GetAsync
asset = await service.UpdateAsync(themeId, assetId, asset);
```
