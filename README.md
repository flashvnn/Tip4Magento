# Tip4Magento
Tips and node for Magento development

##### Get Product Manufacturer information
```php
echo $_product->getAttributeText('manufacturer');
```
##### Get block class name
```php
Mage::getConfig()->getBlockClassName('catalog/product_view_media');
```
##### Add class to body
Use xml
```xml
<reference name="root">
            <action method="addBodyClass"><classname>resource-library-home</classname></action>
</reference>
```
Use PHP code
```php
if ($root = $this->getLayout()->getBlock('root')) {
    $root->addBodyClass('whatever');
}
```
##### Enable swatches images keep frame on page difference product list
```php
// create alternative template file of  configurableswatches/catalog/media/js.phtml and change $this->getProductImageFallbacks() to $this->getProductImageFallbacks(true)
<script type="text/javascript">
    $j(document).on('product-media-loaded', function() {
        ConfigurableMediaImages.init('<?php echo $this->getImageType(); ?>');
        <?php foreach ($this->getProductImageFallbacks(true) as $imageFallback): ?>
        ConfigurableMediaImages.setImageFallback(<?php echo $imageFallback['product']->getId(); ?>, $j.parseJSON('<?php echo $imageFallback['image_fallback']; ?>'));
        <?php endforeach; ?>
        $j(document).trigger('configurable-media-images-init', ConfigurableMediaImages);
    });
</script>

```
