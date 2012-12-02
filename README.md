css-template-layout
===================

JavaScript (jQuery) implementation of the CSS Template Layout Module

This is fork of [http://code.google.com/p/css-template-layout/](project on google code).

I this version several problems vere fixed, because author did not maintain it since August 2010.

Solved problems:
* Fixed bug with box-sizing: border-box
* Fixed bug with different hights of rows
* If defined function $.showPage it will be used for pade showing instead of internal

I'm not sure that this version corresponds to current W3C version but it works fine for me.

Examples of usage may be found on original project page, I'm using it in such way:

	/**
	* Do not show all transformations for user
	*/
	var  body = $('#body');
	body.css(
		'opacity',
		.0001
	).parent().css({
		'padding'	: 0,
		'overflow'	: 'visible'
	});
	/**
	* Look for all css files, ad process each of them
	*/
	$('link[rel="stylesheet"]').each(function () {
		$.setTemplateLayout($(this).attr('href'));
	});
	/**
	* Set custom function for page showing
	*/
	$.showPage	= function () {
		body.animate(
			{
				'opacity'	: 1
			},
			100
		);
	};
	/**
	 * Update layout after page changes
	 */
	$(document).on('DOMNodeInserted', 'iframe', function() {
		setTimeout($.redoTemplateLayout, 100);
	});
	setInterval($.redoTemplateLayout, 1000);