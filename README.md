Magento-Functions
=================

A Resource of Magento Functions


####Table of Contents
***

1. [Category](#category)
2. [Product](#product)
3. [User](#user)
4. [Cart](#cart)
5. [Checkout](#checkout)
6. [General](#general)
7. [Account](#account)

***


##Category

##Product

####Fetch Product Collection
```php

$collection = Mage::getModel('catalog/product')
              ->getCollection()
              ->addAttributeToSelect('*')
              ->addAttributeToSort('name', 'DESC')
              ->setOrder('name', 'ASC');
```

####Magento Load Products
```php
Individual Product Helper
--------------------------------------------------------------------------------------
$_helper = $this->helper('catalog/output');
$_product = $this->getProduct();

Load Product from Collection
--------------------------------------------------------------------------------------
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

##Checkout


####Shipping
```php
Retrive Shipping Method from Quote
--------------------------------------------------------------------------------------
$rate = Mage::getSingleton('checkout/session')->getQuote()->getShippingAddress()->getShippingRatesCollection();

$rate->getCarrier(); // This will provide you with the carrier code
$rate->getCarrierTitle(); // This will give you the carrier title
$rate->getCode(); // This will give you **current shipping method** code
$rate->getMethod(); // This will provide you with the **shipping method** code
$rate->getMethodTitle(); // This will tell you current shipping method title
$rate->getMethodDescription(); // And this is the description of the current shipping method and **it could be NULL**
```

##General


####Working with Blocks

```
Step 1:
Create your static block
 
Step 2:
Open the file that references the page you intend to put the block into IE‘page.xml’.
 
Step 3:
Add this to the appropriate place in the XML file
 
<block type="cms/block" name="xxxxxx">
  <action method="setBlockId"><block_id>xxxxxx</block_id></action>
</block>
 
Step 4:
Navigate your way to the template folder (app > design > frontend > default > your_theme > template) Open the file that you would like the block to appear in and insert the following code in the appropriate position where xxxxxx is the ‘Identifier’ you set earlier when creating your block.
 
<?php echo $this->getChildHtml('xxxxxx') ?>
 
 
Render Block within .phtml
 
<?php echo $this->getLayout()->createBlock('cms/block')->setBlockId('my-new-block')->toHtml() ?>
```

##Account


####Navigation Links

#####Removing Navigation Links
In local.xml add the following
```
<customer_account>
    <reference name="customer_account_navigation" >
            <action method="removeLinkByName"><name>recurring_profiles</name></action>
            <action method="removeLinkByName"><name>billing_agreements</name></action>
            <action method="removeLinkByName"><name>reviews</name></action>
            <action method="removeLinkByName"><name>downloadable_products</name></action>
            <action method="removeLinkByName"><name>OAuth Customer Tokens</name></action>

            <action method="removeLinkByName"><name>account</name></action>
            <action method="removeLinkByName"><name>account_edit</name></action>
            <action method="removeLinkByName"><name>address_book</name></action>
            <action method="removeLinkByName"><name>orders</name></action>
            <action method="removeLinkByName"><name>tags</name></action>
            <action method="removeLinkByName"><name>wishlist</name></action>
            <action method="removeLinkByName"><name>newsletter</name></action>
    </reference>
</customer_account>

```
#####Adding Navigation Links
In local.xml add the following
```
<customer_account>
    <reference name="customer_account_navigation">
        <action method="addLink">
            <name>my_new_section</name>
            <path>module/index/index</path>
            <!-- <url>http://mydomain.com</url> -->
            <label>Module Account View</label>
            <params><_secure>true</_secure></params>
        </action>
    </reference>
</customer_account>
```



