## StorefrontAccessTokens

You can use the StorefrontAccessToken resource to generate storefront access tokens. Storefront access tokens are used to delegate unauthenticated access scopes to clients that need to access the unautheticated Storefront API. A sales channel can generate a storefront access token and then pass it to a consuming client, such as JavaScript or a mobile application.

**There is a hard limit of 100 tokens per Shopify store.**

### Creating a StorefrontAccessToken

To create a StorefrontAccessToken, you must pass in a title for the token. There are no constraints on the uniqueness of the title. 

```cs
var service = new StorefrontAccessTokenService(myShopifyUrl, shopAccessToken);
var token = await service.CreateAsync("My storefront access token");
```

### Deleting a StorefrontAccessToken

```cs
var service = new StorefrontAccessTokenService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(storefrontAccessTokenId);
```

### Listing StorefrontAccessTokens

This endpoint is not paginated, because there is a limit of only 100 storefront access tokens per shop.

```cs
var service = new StorefrontAccessTokenService(myShopifyUrl, shopAccessToken);
var list = await service.ListAsync();
```