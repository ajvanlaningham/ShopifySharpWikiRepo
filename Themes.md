## Themes

The `ThemeService` lets you create, update, list, get and delete a store's themes.

### Creating a theme

When you create a theme, you can optionally pass in a URL that points to a .zip file containing all of the new theme's files. Shopify will then copy those files into the theme. Be aware that copying files is not instant, and the theme's `Processing` flag will be set to `true` until it's done.

You cannot update or delete a theme that is still processing.

```c#
var service = new ThemeService(myShopifyUrl, shopAccessToken);
var theme = new Theme()
{
    Name = "My new theme.",
    Role = "unpublished"
}

theme = await service.CreateAsync(theme);

//Or, create a theme and copy its files from a .zip file URL
theme = await service.CreateAsync(theme, 'https://my-domain.com/my-theme-files.zip');
```

### Retrieving a theme

```c#
var service = new ThemeService(myShopifyUrl, shopAccessToken);
var theme = await service.GetAsync(themeId);
```

### Updating a theme

Remember, you can't update a theme if its `Processing` flag is set to `true`. Shopify will automatically set it to `false` once it's done processing. Additionally, you cannot set a theme's role from `"main"` to `"unpublished"`. Instead, you need to set a different theme's role to `"main"`.

```c#
var service = new ThemeService(myShopifyUrl, shopAccessToken);
var theme = await service.UpdateAsync(themeId, new Theme()
{
    Role = ThemeRole.Main,
    Name = "My updated theme."
});
```

### Deleting a theme

```c#
var service = new ThemeService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(themeId);
```

### Listing themes

```c#
var service = new ThemeService(myShopifyUrl, shopAccessToken);
var themes = await service.ListAsync();
```
