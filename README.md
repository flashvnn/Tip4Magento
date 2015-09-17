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
##### How to specify custom sort order for product collection?
http://magento.stackexchange.com/questions/10031/how-to-specify-custom-sort-order-for-product-collection
```php
/* @var $collection Mage_Catalog_Model_Resource_Product_Collection */
$collection = Mage::getModel('catalog/product')
    ->getCollection()
    ->addAttributeToSelect('*')
    ->addAttributeToFilter('status', 1)
    ->addAttributeToFilter('entity_id', array(
            'in' => $productIds,
        ));

$collection->getSelect()->order(new Zend_Db_Expr('FIELD(e.entity_id, ' . implode(',', $productIds).')'));

foreach($collection as $product) {
    var_dump($product->getId());
}
```
