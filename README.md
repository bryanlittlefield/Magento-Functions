Magento-Functions
=================

A Resource of Magento Functions


####Table of Contents
***

1. [Catalog](#catalog)
	* [Product](#product)
	* [Category](#category)
2. [User](#user)

***


##Catalog

###Category

###Product

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
