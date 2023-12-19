## Webhooks

### Creating a webhook

```c#
var service = new WebhookService(myShopifyUrl, shopAccessToken);
Webhook hook = new Webhook()
{
    Address = "https://my.webhook.url.com/path",
    CreatedAt = DateTime.Now,
    Fields = new List<string>() { "field1", "field2" },
    Format = "json",
    MetafieldNamespaces = new List<string>() { "metafield1", "metafield2" },
    Topic = "app/uninstalled",
};

hook = await service.CreateAsync(hook);
```

### Retrieving a webhook

```c#
var service = new WebhookService(myShopifyUrl, shopAccessToken);
var webhook = await service.GetAsync(webhookId);
```

### Updating a webhook

```c#
var service = new WebhookService(myShopifyUrl, shopAccessToken);
var webhook = await service.UpdateAsync(webhookId, new Webhook()
{
    Address = "https://my.webhook.url.com/new/path
});
```

### Deleting a webhook

```c#
var service = new WebhookService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(webhookId);
```

### Counting webhooks

```c#
var service = new WebhookService(myShopifyUrl, shopAccessToken);
int webhookCount = await service.CountAsync();
```

### Listing webhooks

```c#
var service = new WebhookService(myShopifyUrl, shopAccessToken);
IEnumerable<Webhook> webhooks = await service.ListAsync();
```