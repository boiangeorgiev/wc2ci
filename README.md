WooCommerce Library for CodeIgniter
===================================

Based on the [WooCommerce API Client Class](https://github.com/helpforfitness/WooCommerce-REST-API-Client-Library-v2.git)
fork from [Guillermo Gette](https://github.com/guillegette)

## About

A Library class for CodeIgniter, implementing the PHP wrapper for the WooCommerce REST API.
Easily interact with the WooCommerce REST API using this wrapper class.
Feedback and bug reports are appreciated.

For more information about the WooCommerce parameters,
visit their [documentation](http://woothemes.github.io/woocommerce-rest-api-docs/ "WooCommerce REST API Documentation v2")

## Requirements

* PHP 5.2.x
* cURL
* WooCommerce 2.1 at least on the store

## Getting started

1. Place the Library inside the `application/libraries` folder.
2. Generate API credentials (Consumer Key & Consumer Secret) on *your profile* page for the store you want to interact with.
3. Initialize the class by loading the Library and setup your API credentials

```php
<?php
	// Setup API credentials
	$params = array(
		__CUSTOMER_KEY_HERE__, // Add your own Consumer Key here
		__CUSTOMER_SECRET_HERE__, // Add your own Consumer Secret here
		__STORE_URL_HERE__, // Add the home URL to the store you want to connect to here
		__IS_SSL__, // TRUE if this store uses SSL (optional)
	);

	// Initialize the class
    $this->load->library('WooCommerce',$params);
?>
```
or do this separately if you're going to connect to several stores.
```php
<?php
	// Initialize the class
    $this->load->library('WooCommerce');

    $consumer_key = __CUSTOMER_KEY_HERE__; // Add your own Consumer Key here
	$consumer_secret = __CUSTOMER_SECRET_HERE__; // Add your own Consumer Secret here
	$store_url = __STORE_URL_HERE__; // Add the home URL to the store you want to connect to here

	// Setup API credentials
	$this->woocommerce->api( $consumer_key, $consumer_secret, $store_url );

	// ...
	// do some business with the store here
	// ...


	// Connect to second store

    $consumer_key = __CUSTOMER_KEY_2__; // Add your own Consumer Key here
	$consumer_secret = __CUSTOMER_SECRET_2__; // Add your own Consumer Secret here
	$store_url = __STORE_URL_2__; // Add the home URL to the store you want to connect to here

	// Setup API credentials
	$this->woocommerce->api( $consumer_key, $consumer_secret, $store_url );

	// ...
	// do some business with the second store here
	// ...
?>
```

### Get the data using methods
```php
<?php
	// Get all orders
	$orders = $this->woocommerce->get_orders();
	print_r( $orders );
?>
```

**All methods return the data `json_decode()` by default so you can access the data.**

## Available methods

### API method

- `api()` - initialize connection with a new store

### Index method

- `get_index()`

### Order methods

- `get_orders()`
- `get_orders( $params = array( 'status' => 'completed' ) )`
- `get_order( $order_id )`
- `get_orders_count()`
- `get_order_notes( $order_id )`
- `update_order( $order_id, $data = array( 'status' => 'processing' ) )`
- `update_order( $order_id, $data = array( 'status' => 'processing', 'note' => 'This is a note') )`

### Coupon methods

- `get_coupons()`
- `get_coupon( $coupon_id )`
- `get_coupon_by_code( $coupon_code )`
- `get_coupons_count()`

### Customer methods

- `get_customers()`
- `get_customers( $params = array( 'filter[created_at_min]' => '2013-12-01' ) )`
- `get_customer( $customer_id )`
- `get_customers_count()`
- `get_customer_orders( $customer_id )`

### Product methods

- `get_products()`
- `get_products( $params = array( 'filter[created_at_min]' => '2013-12-01' ) )`
- `get_product( $product_id )`
- `get_products_count()`
- `get_product_reviews( $product_id )`

### Report methods

- `get_reports()`
- `get_sales_report( $params = array( 'filter[start_date]' => '2013-12-01', 'filter[end_date]' => '2013-12-09' ) )`
- `get_top_sellers_report( $params = array( 'filter[limit]' = '10' ) )`

### Custom endpoints

If you extended the WooCommerce API with your own endpoints you can use the following function to get access to that data
- `make_custom_endpoint_call( $endpoint, $params = array(), $method = 'GET' )`

## Changelog

**version 1.0 - 2015-03-25**

- Initial release

## Credit

- Copyright (c) 2015 - Boian Georgiev
- Copyright (c) 2013-2014 - [Gerhard Potgieter](http://gerhardpotgieter.com/)
- Released under the [GPL3 license](http://www.gnu.org/licenses/gpl-3.0.html)
