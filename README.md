# All Rejection Issues of WordPress Theme in ThemeForest:

## Please use a unique theme name.

## Please use a unique prefix:
Please use a unique prefix for all function names, custom images sizes, classes, constants, hooks, public/global variables, and database entries to avoid conflict issues with plugins and other themes. Ref: [http://themereview.co/prefix-all-the-things/](http://themereview.co/prefix-all-the-things/) 

* Function names should be prefixed
* Image sizes added via `add_image_size()` function. All image size names should also be prefixed with that same prefix. 
* All global variable names. Add a prefix to all variable names that you declare outside a function scope. 

While prefixing, please remember that refixes should consist of either your `themename_`, `authorname_`, or `frameworkname_`

**_Example(s):_**
	
```php
$themename_variable = "something";
	
function name themename_whatever(){
	//your function body goes here
}
	
add_action( 'after_setup_theme', 'themename_setup' );
	
function themename_setup(){
	add_image_size("themename_single_blog", 1170, 650);
}
```


## All dynamic data must be correctly escaped:
All dynamic data must be correctly escaped for the context where it is rendered. Please perform a global search for “echo $” and you will see several issues. Ref: [https://vip.wordpress.com/documentation/vip/best-practices/security/validating-sanitizing-escaping/](https://vip.wordpress.com/documentation/vip/best-practices/security/validating-sanitizing-escaping/) 

**_Example(s):_**
[http://envato.d.pr/BVYZr](http://envato.d.pr/BVYZr) 




