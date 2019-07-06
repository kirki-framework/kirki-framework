---
layout: doc
title: js_vars
---

{% include alert.html style="danger" text="Use the output argument and set transport to auto instead of using the js_vars argument. Using js_vars is almost never needed. This argument should only be used in special cases as it will be internally calculated from the output argument." %}

If you set `transport` to `postMessage` you can write your own scripts, or you can use the `js_vars` argument and let Kirki automatically create these for you.

It is defined as an array of arrays so you can specify multiple elements.

```php
new \Kirki\Field\Color( [
	'settings'  => 'my_setting',
	'label'     => esc_html__( 'Text Color', 'textdomain' ),
	'section'   => 'my_section',
	'default'   => '#333',
	'transport' => 'postMessage',
	'js_vars'   => [
		[
			'element'  => 'body',
			'function' => 'css',
			'property' => 'color',
		],
		[
			'element'  => 'h1, h2, h3, h4',
			'function' => 'css',
			'property' => 'color',
		],
	]
] );
```

Available arguments you can use on each item inside each array:

* `'element'` (string): The CSS element you want to affect.
* `'function'` (string): Can be `'css'`,`'html'` or `'style'`:
	* `css`: Changes the affected elements directly with inline styles
	* `style`: Will add a `'<style>'`element to the `'<head>'`section of your Customizer live preview with styles set for `'element'` and `'property'`. Recommend if you want to live preview for example `'a:hover'`, pseudo-element or style changes that might conflict with existing styles.
	* `html`: Outputs the option value to `'element'` and replaces existing text or html.
* `'property'` (string): If you set `'function'` to `'css'` or `'style'` then this will allow you to select what CSS you want applied to the selected `'element'`.
* `units` (string): In some cases you may want to add units. The string entered here will be appended to the value. Example: If you have a slider control that should change the border-radius of an element, then you will have to use `px` or `%` as units since sliders output a simple numeric value.
* `prefix` (string): Will be used before the value
* `suffix` (string): Will be used after the value and units.
