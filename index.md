---
layout: page
title: WordPress Standards
---

Since the bulk of our code is for the WordPress platform and much of it is also reviewed by WordPress.com VIP, this is the most important platform to have consistency on.
Source link: [WordPress Coding Standards](http://codex.wordpress.org/WordPress_Coding_Standards)
Also see our WordPress Best Practices document.

## PHP Formatting:

#### Whitespace:

* Always use TABS instead of SPACES to indent code:
This reduces code size and allows everyone to choose their preferred tab stop width.
Exception: Indenting within a line. This should always be done with SPACES so that things line up the same for everybody.

* NEVER leave whitespace at the end of a line, or have whitespace on an empty line.
Your text editor should be able to display whitespace. Turn on this option to show where the whitespace is.

* Use whitespace appropriately and consistently. Blocks of related code should be grouped and separated by blank lines.

* The standards below differ from the official WordPress coding standards:

Whitespace should be used around ALL binary operators, but NOT after unary operators like ! or -. Thus:

{% highlight php startinline %}
if( 'bar ' . 'bacon' == 'bar bacon' && !$truth_serum ) {
  // Code
}
{% endhighlight %}


Whitespace should not be given inside array indices, but any expressions within should follow the above whitespace rules:
{% highlight php startinline %}
$foo = array( 'bar' => 'baz', 5 => 'five' );
$bar = $foo['bar'];  // NOT $foo[ 'bar' ];
$five = $foo[3 + 2]; // NOT $foo[3+2];
{% endhighlight %}

#### Blocks
Control blocks must be written as such:
{% highlight php startinline %}
if( $x == 'bar' ) {
  // Code
}
{% endhighlight %}

* That is, control statement, NO SPACE, open-parenthesis, SPACE, statement, SPACE, close-parenthesis, SPACE, open-brace, NEWLINE.

#####NEVER EVER EVER EVER EVER use the alternate PHP control statement syntax:
{% highlight php startinline %}
if( $foo ) :
endif;
while( $condition ) :
endwhile;
{% endhighlight %}

* This leads to code that is less consistent and harder to read. There's no reason you must write it this way for "the loop." Break the habit.

* Closing braces should ALWAYS appear on their own line. (This differs from WP coding standards)

Control blocks should always be written with braces:
{% highlight php startinline %}
if( $condition ) {
  $foo = 'bar';
}

if( $x == 'bar' ) {
   $foo = 'bar';
}
elseif( $x == 'baz' ) {
  $foo = 'quux';
}
else {
  $foo = 'brains';
}
{% endhighlight %}

####PHP: The One True Singleton
This singleton is the most robust and compact implemetation I have found. It prevents multiple instantiation explicitly. We should always use this for any singletons in the future.
{% highlight php startinline %}
class Theme_Feature {
  // Define and register singleton
  private static $instance = false;
  public static function instance() {
    if( !self::$instance )
      self::$instance = new Theme_Feature; // MUST BE UPDATED WITH CLASS NAME
    return self::$instance;
  }
  // Disallow clone() of object
  private function __clone() { }
  // CPT registration, custom taxonomy registration, actions, filters
  private function __construct() { }
}
Theme_Feature::instance();

{% endhighlight %}

####HTML
HTML should be indented with TABS, not SPACES, much like PHP.
HTML intermingled with PHP should start at the same indentation level as the PHP.
HTML embedded in PHP should for the most part be written OUTSIDE of PHP blocks.
Short tags made up of many parts can be built in PHP.

If you need to capture long chunks of HTML into an output, use ob_start() and ob_get_clean():
{% highlight php %}
<?php ob_start(); ?>
  <p>
    This is a long piece of <span class="<?php echo esc_attr( join( ' ', $classes ) ); ?>">some text</span>
    that should be captured by <em>ob_start()</em> and <em>ob_get_clean()</em>
   </p>
<?php $markup = ob_get_clean(); ?>
{% endhighlight %}

* HTML attribute values must ALWAYS be written with double-quotes, and always lower-case, with no spacing: attr="value"

Correct
{% highlight html %}
<div class="foo bar"></div>
{% endhighlight %}
Incorrect
{% highlight html %}
<DIV class='foo bar'></DIV>
{% endhighlight %}

Any PHP variables emitted into HTML must ALWAYS be escaped with one of the escaping functions: esc_html() or esc_attr()
Javascript variables should be set using encode_json() over esc_js(). json_encode() is more type-safe and can bring over any type of variable into a Javascript representation and will quote properly when necessary:
{% highlight php startinline %}
<script>var foo = <?php echo json_encode( $foo ); ?>;</script>
{% endhighlight %}

Within WordPress, JavaScript variables should be provided to the page using wp_localize_script() instead of direct injection of JavaScript code as above.

#### Translation Strings
Unless a theme needs to be translation-ready, there's never any need to leave the _e(), __(), esc_attr_e(), or other translation functions in the theme as they serve no purpose but to slow down page rendering.

#### URLs

WordPress includes myriad functions for building URLs, and these should always be used instead of manual URL construction.

* For front-end URLs, home_url() is used to build URLs relative to the site URL.
* For admin URLs, admin_url() is used to build URLs relative to the site's WP Admin.
* If query strings are needed, add_query_arg() should always be used, in conjunction with the aforementioned URL functions.
* If URLs are to be constructed from more than two pieces (base URL and relative path thereto), path_join() should be used. Note that the second parameter cannot contain a leading slash, otherwise path_join() will return only the second argument.

When referencing files within the theme, the following two functions should be used:

* get_stylesheet_directory_uri() - for child themes or themes that won't have parent/child setup
* get_template_directory_uri() - only to be used in a parent/child theme setup when the parent theme is referenced

Related to the foregoing statement, bloginfo() and get_bloginfo() should never be used to reference theme directories.

Root-relative URLs should never be used as we can hardly predict what a client may do with a site once we deliver a final product to them.
