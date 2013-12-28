# WooCommerce Compatibility Utility Class

The purpose of this class is to provide a single point of compatibility functions for dealing with supporting multiple versions of WooCommerce.

## How to Use

The recommended procedure is to include this class in any plugin that you want to add WooCommerce cross-compatibility to, renaming the file/class, replacing "my plugin" with the name of the plugin in which this is included, so as to avoid clashes between plugins.

Over time it's expected that methods will be removed as compatibility for older versions of WooCommerce is dropped.

The class also provides a convenient reference of methods, constants, etc, that need to be modified within a plugin for WooCommerce cross-compatibility.
