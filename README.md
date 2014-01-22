# WooCommerce 2.1 Compatibility Utility Class

The purpose of this class is to provide a single point of compatibility functions for dealing with supporting multiple versions of WooCommerce (currently 2.0.x and 2.1)

## How to Use

The recommended procedure is to include this class in any plugin that you want to add WooCommerce cross-compatibility to, renaming the file/class, replacing "my plugin" with the name of the plugin in which this is included, so as to avoid clashes between plugins.

Over time it's expected that methods will be removed as compatibility for older versions of WooCommerce is dropped.

The class also provides a convenient reference of methods, constants, etc, that need to be modified within a plugin for WooCommerce cross-compatibility.

## Changelog

**1.1 - 2014.01.22**

* Feature - Added a bunch of new compatibility methods
* Fix - Fixed get_order_custom_field() method

**1.0 - 2014.01.17**

* Initial release

## Compatibility Issues

### Fixed

* `Woocommerce::add_inline_js()` -> `wc_enqueue_js()` (Use `WC_My_Plugin_Compatibility::wc_enqueue_js()`)
* `$woocommerce->force_ssl()` has been replaced with `WC_HTTPS::force_https_url()`, [WC commit ref](https://github.com/woothemes/woocommerce/commit/807534095e676722f4d27931b10eed9b906d5baa) (Use `WC_My_Plugin_Compatibility::force_https_url()`)
* `Woocommerce::add_error($msg)` is gone.  The equivalent is `wc_add_notice( $msg, 'error' )` [WC issue](https://github.com/woothemes/woocommerce/pull/4099) (Use `WC_My_Plugin_Compatibility::wc_add_notice()`)
* `WooCommerce::add_message($msg)` is gone.  The equivalent is `wc_add_notice( $msg )` (Use `WC_My_Plugin_Compatibility::wc_add_notice()`)
* `Woocommerce::attribute_label()` is gone.  The equivalent is `wc_attribute_label()` (Use `WC_My_Plugin_Compatibility::wc_attribute_label()`)
* `WOOCOMMERCE_VERSION` -> `WC_VERSION` (Use `WC_My_Plugin_Compatibility::get_wc_version()`)
* `WC_Order::get_shipping()` -> `WC_Order::get_total_shipping()` (Use `WC_My_Plugin_Compatibility::get_total_shipping()`)
* `WC_Order::$order_custom_fields` is gone, replaced by magic getter methods (Use `WC_My_Plugin_Compatibility::get_order_custom_field()`)
* `WooCommerce::logger()` -> `new WC_Logger()` (Use `WC_My_Plugin_Compatibility::new_wc_logger()`)
* Payment Gateway configuration url changed from `/wp-admin/admin.php?page=woocommerce_settings&tab=payment_gateways&section=WC_Gateway_Intuit_QBMS_Credit_Card` to `/wp-admin/admin.php?page=wc-settings&tab=checkout&section=wc_gateway_intuit_qbms_credit_card`  (Use `WC_My_Plugin_Compatibility::get_payment_gateway_configuration_url()` and `WC_My_Plugin_Compatibility::is_payment_gateway_configuration_page()`)
* Shipping Method configuration url changed (Use `WC_My_Plugin_Compatibility::get_shipping_method_configuration_url()` and `WC_My_Plugin_Compatibility::is_shipping_method_configuration_page()`)
* `woocommerce_format_total()` -> `wc_format_decimal()` (Use `WC_My_Plugin_Compatibility::wc_format_decimal()`)
* `Woocommerce::error_count()`, `Woocommerce::message_count()` -> `wc_notice_count()` (Use `WC_My_Plugin_Compatibility::wc_notice_count()`)
* `global $woocommerce;` -> `WC()` (Use `WC_My_Plugin_Compatibility::WC()`)
* `WC_Order::$shipping_method` is gone.  `WC_Order::get_shipping_methods()` and `WC_Order::has_shipping_method()` are added  (Use `WC_My_Plugin_Compatibility::get_shipping_method_ids()` and `WC_My_Plugin_Compatibility::has_shipping_method()`)
* Session var `chosen_shipping_method` (int shipping method id) -> `chosen_shipping_methods` (associative array of shipping package index to int shipping method id) (Use `WC_My_Plugin_Compatibility::get_chosen_shipping_methods()`)
* `Coocommerce->show_messages()` -> `wc_print_notices()` (Use `WC_My_Plugin_Compatibility::wc_print_notices()`)

### Not Fixed

* Address Validation - fix display based on #shiptobilling input [WC commit ref](https://github.com/woothemes/woocommerce/commit/ac51ebf2b80c1303af74c65602e882fce314cc5f)
* Pay and Thanks page are now endpoints, not actual pages. Affects gateways and anything with checkout handling. [WC commit ref] (https://github.com/woothemes/woocommerce/commit/e4f4b09ba6f40456bbca413383324b23c0fcd3a6), e.g order received URLs now look like `http://wcdev.com/checkout/order-received/102/?key=order_5274642282533`  Rather than `woocommerce_get_page_id( 'pay' )` use `WC_Order::get_checkout_payment_url()` or `WC_Order::get_checkout_order_received_url()` instead
* New `taxonomy_is_product_attribute()` function to use instead of checking for `pa_` prefix [WC commit ref](https://github.com/woothemes/woocommerce/commit/cde4947acf4bf76cbc534dc63a638c4e5ee31dfe)
* Reports are being refactored [WC issue] (https://github.com/woothemes/woocommerce/issues/3281)
* `clear_product_transients` is refactored in classes [WC issue](https://github.com/woothemes/woocommerce/issues/3282)
* No more `?add-to-cart` redirect, uses `POST`, [WC commit ref](https://github.com/woothemes/woocommerce/commit/b38ef8efcd32694f9a7962c7435e5fd238341584)
* Admin Product Data Tabs are now filterable, [WC commit ref](https://github.com/woothemes/woocommerce/commit/0204ff231a0acf01c50c30ec100e7059ad41b862)
* Admin files have been moved into includes directory, [WC commit ref](https://github.com/woothemes/woocommerce/commit/8a6ff89bf1ebceecec6f20401abde99b9c54cca3)
* Increase/Decrease stock functions have been replaced by global set_stock, [WC commit ref](https://github.com/woothemes/woocommerce/commit/d021980c10bdac699437254090ba1159a9ddfc6e)
* Icons have been converted into fonts, [WC commit ref](https://github.com/woothemes/woocommerce/commit/e6304f881bd19ec15abb890be80e78cf72fd40c0)
* Extensions can add their template to the status screen to check if they're being overridden [WC commit ref](https://github.com/woothemes/woocommerce/pull/3845)
* New `price` WC form input type [WC commit ref](https://github.com/woothemes/woocommerce/commit/b8928153369e14d4744dc0467ed7dc94403692fe)
* `WC_Order::$shipping_method_title` is gone
* `woocommerce_meta_boxes_save_errors()` is gone.  The equivalent is `WC_Admin_Meta_Boxes::save_errors()` but I don't think it's too helpful since it's an instance method and it wouldn't really make sense to extend that class

### Won't Fix

* Settings have been refactored / changed, `Payment Gateway` now called `Gateway Display`?, [WC commit ref](https://github.com/woothemes/woocommerce/commit/3d078397b33629b8f64de714679da8d758be4f12)
* Downloadable file changes [WC commit ref](https://github.com/woothemes/woocommerce/commit/96a7a4b7307207234ec8b74b4e888e7056f14360), [Issue ref](https://github.com/woothemes/woocommerce/issues/3812)
* Add to cart URLs/text has changed [WC commit ref](https://github.com/woothemes/woocommerce/commit/ef49977905d840329afb9b447f2c4729f347da5d#commitcomment-4179036)
* Gateways can use a default credit card form that uses jQuery.Payment [WC commit ref](https://github.com/woothemes/woocommerce/commit/72c00a601aa3e623de3d5cf817c87129175ce933)
* `woocommerce_loop_add_to_cart_link` filter signature changed
* `WC_Order::get_total()`, `WC_Order::get_total_shipping()`, `WC_Order::get_total_tax()`, `WC_Order::get_shipping_tax()`, `WC_Order::get_cart_tax()`, `WC_Order::get_order_discount()`, `WC_Order::get_cart_discount()` no longer returns currency format, ie rather than 1.00 now 1 is returned (Use `WC_My_Plugin_Compatibility::wc_format_decimal()`)
* `Woocommerce::nonce_field()` is deprecated, use `wp_nonce_field( 'woocommerce-' . $action, '_n', $referer = true, $echo = true )` instead for 2.0.x style behavior
