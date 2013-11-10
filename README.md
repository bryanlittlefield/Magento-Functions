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

```php
<!-- ************************* Fetch Product and Info ************************* -->
<?php $_helper = $this->helper('catalog/output'); ?>
<?php $_product = $this->getProduct(); ?>
<!-- ======================================================================== -->
<?php
$model = Mage::getModel('catalog/product') //getting product model
$_product = $model->load($productid); //getting product object for particular product id
?>


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

