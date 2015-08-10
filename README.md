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
