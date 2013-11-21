Magento-Functions
=================

A Resource of Magento Functions


####Table of Contents
***

1. [Category](#category)
2. [Product](#product)
3. [User](#user)
4. [Cart](#cart)

***


##Category

##Product

####Fetch Product

```php

Individual Product Helper
--------------------------------------------------------------------------------------
$_helper = $this->helper('catalog/output');
$_product = $this->getProduct();

Global Product Helper
--------------------------------------------------------------------------------------
$_product = Mage::getModel('catalog/product')->load($productid); //getting product object for particular product id
$_product = Mage::getModel('catalog/product')->load($this->getProduct()->getId());
$_attributes = $_product->getAttributes();
```

####Magento Load Product By Name / SKU / ID
```php
// Load by name
$_product = Mage::getModel('catalog/product')->loadByAttribute('name', 'product_name');

// Load by SKU
$_product = Mage::getModel('catalog/product')->loadByAttribute('sku', '234SKU93');

//Load by ID (just load):
$_product = Mage::getModel('catalog/product')->load($productID);
```

####Fetch Default Product Info
```php
<?php
echo $_product->getShortDescription(); //product's short description
echo $_product->getDescription(); // product's long description
echo $_product->getName(); //product name
echo $_product->getSku(); //product Sku
echo $_product->getPrice(); //product's regular Price
echo $_product->getSpecialPrice(); //product's special Price
echo $_product->getProductUrl(); //product url
echo $_product->getImageUrl(); //product's image url
echo $_product->getSmallImageUrl(); //product's small image url
echo $_product->getThumbnailUrl(); //product's thumbnail image url
echo $_product->getAvailability(); //product's thumbnail image url     
?>
```

####Custom Product Attributes
```php
For drop-down Product Attributes use the following code 
--------------------------------------------------------------------------------------
<?php echo $_product->getAttributeText('attribute_name') ?>


For all other Product Attribute types
--------------------------------------------------------------------------------------
<?php echo $_product->getAttributeName() ?>

-or-

<?php echo $_product['attribute_name'];?>


Display Product Attributes Globally
--------------------------------------------------------------------------------------
<?php if($product->getResource()->getAttribute('ATTRIBUTE_CODE_HERE')->getFrontend()->getValue($product)) : ?> 

 <?php echo 'Attribute Title: '.$product->getResource()->getAttribute('ATTRIBUTE_CODE_HERE')->getFrontend()->getValue($product); ?>  

<?php endif; ?>
```

##User
```php
/* Check if the customer is logged in or not */
if (Mage::getSingleton('customer/session')->isLoggedIn()) {
 
    /* Get the customer data */
    $customer = Mage::getSingleton('customer/session')->getCustomer();
    /* Get the customer's full name */
    $fullname = $customer->getName();
    /* Get the customer's first name */
    $firstname = $customer->getFirstname();
    /* Get the customer's last name */
    $lastname = $customer->getLastname();
    /* Get the customer's email address */
    $email = $customer->getEmail();
 
}
```

##Cart
```php
/* Get all the items in the cart */
$cartItems = Mage::getSingleton('checkout/session')->getQuote()->getAllItems();
/* Iterate through the items */
foreach ($cartItems as $item) {
 /* Load the product and get the custom attribute */
 Zend_Debug::dump(Mage::getModel('catalog/product')->load($item->getProduct()->getId())->getMyCustomAttribute());
}
```

