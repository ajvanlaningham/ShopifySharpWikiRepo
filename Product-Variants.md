## Product Variants

A product variant is a different version of a product, such as differing sizes or differing colors. Without product variants, you would have to treat the small, medium and large versions of a t-shirt as three separate products; product variants let you treat the small, medium and large versions of a t-shirt as variations of the same product.

### Creating a Product with a variant in one go

```cs
 var product = new Product()
 {
     Title = "Test Product Walter",
     Vendor = "Burton",
     BodyHtml = "<strong>Good snowboard!</strong>",
     ProductType = "Snowboard",
     Images = images,
     //Make sure to give your product the correct variant option
     Options = new List<ProductOption>
     {
         new ProductOption
         {
             Name = "Color"
         }
     },
     //And then create a collection of variants or assign the "Variants" property
     //to an already defined collection.
     Variants = new List<ProductVariant>
     {
         new ProductVariant
         {
             Option1 = "Black",
         },
         new ProductVariant
         {
             Option1 = "Green",
         },
     }
 };
```

### Creating a Product Variant

```cs
var service = new ProductVariantService(myShopifyUrl, shopAccessToken);
var variant = await service.CreateAsync(productId, new ProductVariant()
{
    Option1 = "blue",
    Price = 123.45,
});
```

### Getting a Product Variant

```cs
var service = new ProductVariantService(myShopifyUrl, shopAccessToken);
var variant = await service.GetAsync(variantId);
```

### Updating a Product Variant

```cs
var service = new ProductVariantService(myShopifyUrl, shopAccessToken);
var variant = await service.UpdateAsync(variantId, new Variant()
{
    Price = 543.21
});
```

### Listing Product Variants

```cs
var service = new ProductVariantService(myShopifyUrl, shopAccessToken);
var variants = await service.ListAsync(productId);
```

### Counting Product Variants

```cs
var service = new ProductVariantService(myShopifyUrl, shopAccessToken);
var count = await service.CountAsync(productId);
```

### Deleting a Product Variant

```cs
var service = new ProductVariantService(myShopifyUrl, shopAccessToken);

await service.DeleteAsync(productId, variantId);
```