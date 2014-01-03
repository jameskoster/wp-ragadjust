=== WP ragadjust ===
Contributors: jameskoster
Tags: typography, rag, hyphenation, preposition
Requires at least: 3.3
Tested up to: 3.8
Stable tag: 1.0.0
License: GPLv2 or later
License URI: http://www.gnu.org/licenses/gpl-2.0.html

Includes ragadjust.js to add subtle improvements to your typography.

== Description ==

WP ragadjust is an extremely simple plugin that includes ragadjust.js on your web pages. Ragadjust.js is a script written by @nathanford and envisaged by @markboulton which resolves several typographical violations relating to the rag that are common on the web:

* Line breaks immediately following a preposition
* Line breaks immediately following a dash
* Small words at the end of a line
* Consecutive hyphenation
* (Line) broken, short emphasised phrases

Solving these issues improves the overall readability of your content.

<a href="http://24ways.org/2013/run-ragged/">Read the article behind the idea</a>.

== Installation ==

1. Upload `wp-ragadjust` to the `/wp-content/plugins/` directory
2. Activate the plugin through the 'Plugins' menu in WordPress
3. Done!

== Frequently Asked Questions ==

= Which elements are _ragadjust_ed by default? =

By default ragajust is applied to `p` tags.

= Can I change which elemnts are adjusted? =

Yes, you can use the `wpr_elements` filter to make adjustments to the selectors.

To add a new selector:

`add_filter( 'wpr_elements', 'wpr_new_selectors' );
function wpr_new_selectors( $elements ) {
	$elements[] .= '.textwidget'; // Adjust text widgets in addition to p
	return $elements;
}
`

To remove a current selector:

`add_filter( 'wpr_elements', 'wpr_remove_elements' );
function wpr_remove_elements( $elements ) {
	unset( $elements['0'] ); // Unset 'p'.
	return $elements;
}`

To use your own, entirely unique selectors:

`add_filter( 'wpr_elements', 'wpr_custom_elements' );
function wpr_custom_elements( $elements ) {
	$elements = array(
			'article',
			'footer',
		);
	return $elements;
}`

These snippets should go in your <a href="http://codex.wordpress.org/Child_Themes">child themes</a> functions.php file.

= Can I change the method used? =

Yes. By default all methods will be used to fix all violations. If however you only want to fix prepositions and ignore everything else you can do so via the `wpr_method` filter like so:

`add_filter( 'wpr_method', 'wpr_custom_method' );
function wpr_custom_method( $method ) {
	$method = 'prepositions';
	return $method;
}`

The method options are:

* _emphasis_ – Text of three or less words in bold or italics does not break across lines.
* _small-words_ – Breaks lines before words of three or less characters.
* _prepositions_ – Breaks lines before prepositions.
* _dashes_ – Breaks lines before hyphens and dashes.
* _all_ (default) - All of the above.

== Screenshots ==

1. Before / After ragadjust.

== Changelog ==

= 1.0.0 =
Initial release.