# All Rejection Issues of WordPress Theme in ThemeForest:

## Please use a unique theme name:



## Theme preview image size:
According to the WordPress org, the dimension of the "screenshot.png" *a.k.a "Theme Preview Image"* inside your theme directory should be of 1200px width and 900px height (1200x900). This is required to display the "theme preview image" properly on **retina / high-dpi** displays. 



## Theme Live preview image size:
Preview image dimension should be 590px X 300px.



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



## Scripts and styles should not be hardcoded:
Scripts and styles should not be hardcoded anywhere in your theme or added any other way but with wp_enqueue_* hook and to be added from the functions file. This includes custom JS/CSS.

For inline styles use: [https://developer.wordpress.org/reference/functions/wp_add_inline_style/](https://developer.wordpress.org/reference/functions/wp_add_inline_style/) and for scripts [https://developer.wordpress.org/reference/functions/wp_add_inline_script/](https://developer.wordpress.org/reference/functions/wp_add_inline_script/)



## Validation errors:
Some of your files contain validation errors (e.g. unclosed tags, nesting errors, duplicate IDs etc) that will need to be fixed. Please be sure that all files validate before resubmitting. 
You can validate HTML at [http://validator.w3.org](http://validator.w3.org)



## Contrast issues:



## No Notices, No Warnings, No Errors:
Please make sure that your theme doesn’t raise any PHP errors, notices or warnings. You should be able to replicate this by enabling wp_debug or installing the Debug Bar plugin: [https://wordpress.org/plugins/debug-bar/](https://wordpress.org/plugins/debug-bar/) 

**_Example(s):_**
	
```php
define('WP_DEBUG', false);
```



## Remove all extraneous text domains:
Remove all extraneous text domains that are completely unrelated to the theme. Please note that packaged PHP libraries (i.e. TGMPA), frameworks, and plugin template text domains are relevant and therefore authorized.


## A screen reader is blank:



## Rename your script and css handles:
If you're enqueueing external css and JavaScript files, you need to rename your style and js handlers inside the `wp_enqueue_script()` function and use meaningful and readable handler names.  

**_Example_**
	
```php
function mythemename_enqueue_js_and_css(){
	wp_enqueue_script( "bootstrap-js", mythemename_get_js_assets_dir()."/bootstrap.js", array("jquery"), null,true );
	wp_enqueue_style( "font-awesome", mythemename_get_css_assets_dir()."/font-awesome.css", null );
}
	
add_action( 'wp_enqueue_scripts', 'mythemename_enqueue_js_and_css' );
	
```
	
For details - [https://github.com/grappler/wp-standard-handles](https://github.com/grappler/wp-standard-handles) 



## Please use '-' instead of '_' or '.' for handlers and remove the extension. 



## The theme should not be modifying the admin-bar styles:



## Documentation display issues:



## The responsive nature of the following elements require improvement:



## Comments Text:
If there are no comments in your WordPress posts, and you want to inform that to your users in your theme, the string must display as "No Comments". 





## No direct enqueueing of jQuery:

If you're enqueueing third party JavaScript files or your theme scipt files, which often depends on jQuery, you should define the dependency via **dependency** param in wp_enqueue_script() function. Don't enqueue jQuery directly or individually, or it will result a soft rejection. Here's an example

**_Example (Don't do this)_**

```php
wp_enqueue_script('jquery'); 
```
	
**_Correct Example_**
	
```php
wp_enqueue_script( "bootstrap-js", mythemename_get_js_assets_dir()."/bootstrap.js", array("jquery"), null,true );
```

Once **jQuery** is definied as a dependency, WordPress will automatically enqueue it from the bundled version of jQuery that ships with WordPress.


## Adding Google Font: 
Whenever we're addding google font(s), we have to make sure that we are following the best practice. We have to add google font in the following way because most of the fonts doesn't support characters from all the languages. 

**_Example_**

``` php
wp_enqueue_style( 'prefix-google-font', prefix_get_google_font_url() );
function prefix_get_google_font_url() {
	$font_url = '';

	/* Translators: If there are characters in your language that are not
	* supported by Arizonia, translate this to 'off'. Do not translate
	* into your own language.
	*/
	$arizonia = _x( 'on', 'Arizonia font: on or off', 'massive' );

	/* Translators: If there are characters in your language that are not
	* supported by Source Sans Pro, translate this to 'off'. Do not translate
	* into your own language.
	*/
	$source_sans_pro = _x( 'on', 'Source Sans Pro font: on or off', 'massive' );

	if ( 'off' !== $arizonia || 'off' !== $source_sans_pro ) {
		$font_families = array();

		if ( 'off' !== $arizonia ) {
			$font_families[] = 'Arizonia';
		}

		if ( 'off' !== $source_sans_pro ) {
			$font_families[] = 'Source Sans Pro:400,300,400italic,600';
		}

		$query_args = array(
			'family' => urlencode( implode( '|', $font_families ) ),
			'subset' => urlencode( 'latin,latin-ext' ),
		);

		$font_url = add_query_arg( $query_args, '//fonts.googleapis.com/css' );
	}

	return esc_url_raw( $font_url );
}
```

	
## No inline scripts and styles: 
You must use css class names and avoid inline css styles (as style attribue). You must also avoid inline JavaScript code through out your theme. Scripts and styles should not be hardcoded anywhere in your theme or added any other way but with `wp_enqueue_*` hook and to be added from the functions file. This includes custom JS/CSS. For inline styles use: [https://developer.wordpress.org/reference/functions/wp_add_inline_style/](https://developer.wordpress.org/reference/functions/wp_add_inline_style/) and for scripts [https://developer.wordpress.org/reference/functions/wp_add_inline_script/](https://developer.wordpress.org/reference/functions/wp_add_inline_script/)




## No commented out code:
This one is pretty straight-forward. If your theme contains commented out code or code blocks, you should remove those before submitting your theme for review. Otherwise, they will get back to you with this same message, again and again. 



## Post password:

if a post is password protected, you should not display the comment section, or any other information that is related to that post, until the password was entered by the user. This also include the number of comments. Check out this function [post_password_required](https://codex.wordpress.org/Function_Reference/post_password_required)


## How to test the blog/posts layout/functionality
How to test the blog/posts layout/functionality - Import the Theme Unit Test [http://codex.wordpress.org/Theme_Unit_Test] file and make sure that:

- Posts display correctly, with no apparent visual problems or errors.
- Posts display in correct order.
- Page navigation displays and works correctly.
- As "sticky posts" are a core feature, the theme should style and display them appropriately.
- Lack of body text should not adversely impact the layout.
- Theme must incorporate both the "Tag" and the "Category" taxonomies in some manner.
- Floats are cleared properly for floated element (thumbnail image) at the end of the post content.




## Contrast:
## Typo:
## Pingbacks & trackbacks should display:
## Language folder is empty:
##  Remove developer notice:


## All default widgets should display correctly:
All default widgets should display correctly in all locations. You can use https://wordpress.org/plugins/monster-widget/ for testing this: http://envato.d.pr/MBc0nf



## Themes execute the presentation:
Themes execute the presentation and styling of content while plugins handle content creation and functionality. Anything users will lose upon switching themes is classified as plugin territory. Here are some common examples:

- Analytics
- SEO options
- Forms
- Non design related meta boxes
- Resource caching
- Dashboard widgets
- Custom Post Types
- Custom Taxonomies
- Shortcodes
- Social media “like”, “follow” and “share” buttons

Anything that falls into plugin territory must be added via a custom plugin. You may use TGM Plugin Activation or equivalent to prompt the user to install the plugin on theme activation, but it cannot be activated without user action.


## The typographic hierarchy of this item requires additional work. For more information, please read:
http://webdesign.tutsplus.com/articles/understanding-typographic-hierarchy--webdesign-11636
Example(s): https://envato.d.pr/4E5uSc


