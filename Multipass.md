## Multipass

Multipass login is for store owners who have a separate website and a Shopify store. It redirects users from the website to the Shopify store and seamlessly logs them in with the same email address they used to sign up for the original website. If no account with that email address exists yet, one is created. There is no need to synchronize any customer databases.

### Creating a Multipass redirect url

To create a multipass redirect url 

```cs
string url = MultipassService.GetMultipassUrl(
	new Customer() {
		Email = "test@example.com",
		MultipassIdentifier = Guid.Tostring(),
		CreatedAt = DateTimeOffset.Now
		....
	},
	Utils.MyShopifyUrl,
	Utils.AccessToken
);
```
