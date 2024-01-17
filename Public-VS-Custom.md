# Using ShopifySharp with a public Shopify app

**Note**: All instances of `shopAccessToken` in the examples below **do not refer to your Shopify API key**.
An access token is the token returned after authenticating and authorizing a Shopify app installation with a
real Shopify store.

All instances of `myShopifyUrl` refer to your users' `*.myshopify.com` URL (although their custom domain should work too).

```cs
var service = new ProductService(myShopifyUrl, shopAccessToken);
```

# Using ShopifySharp with a private Shopify app

ShopifySharp should work out of the box with your private Shopify application, all you need to do is replace the `shopAccessToken` with your private app's password when initializing a ShopifyService:

```cs
var service = new ProductService(myShopifyUrl, privateAppPassword)
```

If you just need an access token for a private Shopify app, or for running the tests in this library, refer
to the **Tests** section below.