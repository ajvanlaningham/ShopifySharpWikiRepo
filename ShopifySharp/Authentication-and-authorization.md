# Using ShopifySharp with a private Shopify app

ShopifySharp should work out of the box with your private Shopify application, all you need to do is replace the `shopAccessToken` with your private app's password when initializing a ShopifyService:

```cs
var service = new ProductService(myShopifyUrl, privateAppPassword)
```

If you just need an access token for a private Shopify app, or for running the tests in this library, refer
to the **Tests** section below.

## Authorization and authentication

**NOTICE**: If you're using ASP.NET MVC5 (or any version that isn't AspNet Core) you'll have compilation errors when trying to pass `Request.QueryString` or `Request.Headers` to the authorization methods described below. [See this issue for a workaround](https://github.com/nozzlegear/ShopifySharp/issues/164).

### Ensure a given URL is a valid \*myshopify.com URL

This is a convenience method that validates whether a given URL is a valid Shopify API domain (the Shopify API is hosted on each individual shop rather than at once central URL). It's great for ensuring
you don't redirect a user to an incorrect URL when you need them to authorize your app installation, and is
ideally used in conjunction with `AuthorizationService.BuildAuthorizationUrl`.

ShopifySharp will call the given URL and check for an `X-ShopId` header in the response. That header is present on all Shopify shops and it's existence signals that the URL is indeed a Shopify URL.

**Note**, however, that this feature is undocumented by Shopify and may break at any time. Use at your own discretion. In addition, it's possible for a malicious site to fake the `X-ShopId` header which would make this method return `true`.

```c#
string urlFromUser = "https://example.myshopify.com";
bool isValidDomain = await AuthorizationService.IsValidShopDomainAsync(urlFromUser).
```

### Build an authorization URL

Redirect your users to this authorization URL, where they'll be prompted to install your app to their Shopify store.

```c#
//This is the user's store URL.
string usersMyShopifyUrl = "https://example.myshopify.com";

// A URL to redirect the user to after they've confirmed app installation.
// This URL is required, and must be listed in your app's settings in your Shopify app dashboard.
// It's case-sensitive too!
string redirectUrl = "https://example.com/my/redirect/url";

//An array of the Shopify access scopes your application needs to run.
var scopes = new List<AuthorizationScope>()
{
    AuthorizationScope.ReadCustomers,
    AuthorizationScope.WriteCustomers
};

//Or, use an array of string permissions
var scopes = new List<string>()
{
    "read_customers",
    "write_customers"
}

//You can find your API key over at https://shopify.dev/tutorials/authenticate-a-private-app-with-shopify-admin
string shopifyApiKey = "";

//All AuthorizationService methods are static.
Uri authUrl = AuthorizationService.BuildAuthorizationUrl(scopes, usersMyShopifyUrl, shopifyApiKey, redirectUrl);
```

### Authorize an installation and generate an access token

Once you've sent a user to the authorization URL and they've confirmed your app installation, they'll be redirected
back to your application at either the default app URL, or the redirect URL you passed in when building the
authorization URL.

The access token you receive after authorizing should be stored in your database. You'll need it to access the
shop's resources (e.g. orders, customers, fulfillments, etc.)

```c#
//The querystring will have several parameters you need for authorization.
string code = Request.QueryString["code"];
string myShopifyUrl = Request.QueryString["shop"];

string accessToken = await AuthorizationService.Authorize(code, myShopifyUrl, shopifyApiKey, shopifySecretKey);
```

### Determine if a request is authentic

Any (non-webhook, non-proxy-page) request coming from Shopify will have a querystring parameter called 'hmac' that you can use
to verify that the request is authentic. This signature is a hash of all querystring parameters and your app's
secret key.

Pass the entire querystring to `AuthorizationService` to verify the request.

```c#
var qs = Request.QueryString;

if(AuthorizationService.IsAuthenticRequest(qs, shopifySecretKey))
{
    //Request is authentic.
}
else
{
    //Request is not authentic and should not be acted on.
}
```

### Determine if a proxy page request is authentic

Nearly identical to authenticating normal requests, a proxy page request only differs in the way the HMAC is generated. All proxy page requests coming from Shopify will have a querystring parameter named `hmac` that you can use to verify the request. This signature is a hash of all querystring parameters and your app's secret key.

```cs
var qs = Request.QueryString;

if(AuthorizationService.IsAuthenticProxyRequest(qs, shopifySecretKey))
{
    //Request is authentic.
}
else
{
    //Request is not authentic and should not be acted on.
}
```

### Determine if a webhook request is authentic

Any webhook request coming from Shopify will have a header called `X-Shopify-Hmac-SHA256` that you can use
to verify that the webhook is authentic. The header is a hash of the entire request body and your app's
secret key.

Pass the entire header collection and the request's input stream to `AuthorizationService` to verify
the request.

```c#
NameValueCollection requestHeaders = Request.Headers;
Stream inputStream = Request.InputStream;

if(AuthorizationService.IsAuthenticWebhook(requestHeaders, inputStream, shopifySecretKey))
{
    //Webhook is authentic.
}
else
{
    //Webhook is not authentic and should not be acted on.
}
```

You can also pass in the request body as a string, rather than using the input stream. However, the request
body string **needs to be identical to the way it was sent from Shopify**. If it has been modified the verification will fail -- even if just one space is in the wrong place.

```c#
NameValueCollection requestHeaders = Request.Headers;
string requestBody = null;

//Reset the input stream. MVC controllers often read the stream to determine which parameters to pass to an action.
Request.InputStream.Position = 0;

//Read the stream into a string
using(StreamReader reader = new StreamReader(Request.InputStream))
{
    requestBody = await reader.ReadToEndAsync();
}

if(AuthorizationService.IsAuthenticWebhook(requestHeaders, requestBody, shopifySecretKey))
{
    //Webhook is authentic.
}
else
{
    //Webhook is not authentic and should not be acted on.
}

```