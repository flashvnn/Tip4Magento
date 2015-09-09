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
