# Remooz - a zoomer function for pictures #

A jQuery plugin that dynamically loads in a larger image so that the user can get a high resolution image. Once the user is in zoom mode they can navigate between a pool of images using thumbnails or navigating via arrows. The zoomer works with spread out images that have a similar class as well as a container with a pool of images.

### Usage ###


Initiate with `$(selector).remooz({'some':'property'});`   
Invoke methods with `$(selector).remooz('method', {'some':'property'});`   
Example

	$('.selector').remooz({
		debug: true,
		zIndex: 2000
	})
 
### HTML ###

Following structure is required for selector to work. (Using Emmet tab complete for full HTML or check /dev/index.html)

*Screen - Full Options*

	div.remooz-fullScreenContainer>div#js-remooz-zoomContainer.remooz-fullScreenContainer-inner+div#js-remooz-zoomThumbnailContainer+div.js-remooz-close.remooz-fullScreenContainer-close.remooz-fullScreenContainer-controller+div.js-remooz-prev.remooz-fullScreenContainer-prev.remooz-fullScreenContainer-controller+div.js-remooz-next.remooz-fullScreenContainer-next.remooz-fullScreenContainer-controller+div.js-remooz-preloader

*Screen - Bare Minimum*

	div.remooz-fullScreenContainer>div#js-remooz-zoomContainer.remooz-fullScreenContainer-inner

*Product Pool*

	div.selector>div#js-remooz-imagePool>img.current+img*2


### Properties ###

#### fitX ####

*Default* `true`   
*Expects* `boolean`

How the zoomed image should react on zoom. fitX means it will not be larger than the window height when zoomed. If used in combination with fitY then this will only allow the image to be the size of the screen proportionally no matter the size of the picture.

	$(selector).remooz({fitX: true})

#### fitY ####

*Default* `false`   
*Expects* `boolean`

How the zoomed image should react on zoom. fitY means it will not be larger than the window height when zoomed. If used in combination with fitX then this will only allow the image to be the size of the screen proportionally no matter the size of the picture.

	$(selector).remooz({fitY: false})

#### srcRegexp ####

*Default* `/\.(jpg|jpeg|png|gif)$/i`   
*Expects* `regexp`

Using regular expressions find the string to be replaced in the original src to get the zoomed image src.

	$(selector).remooz({srcRegexp: /\.(jpg|jpeg|png|gif)$/i})

#### srcStrReplace ####

*Default* `"-large.$1"`   
*Expects* `regexp`

In combination with the above property you can change the src of the full-sized image. This uses the normal javascript `str.replace()` method. You can use $1, $2 to reference brackets etc.

	$(selector).remooz({srcStrReplace: "-large.$1"})

#### useScroll ####

*Default* `false`   
*Expects* `boolean`

If you would like to control the zoom container with scroll instead of moving the mouse up and down. Set this attribute. You'll also need to define overflow's yourself.

	$(selector).remooz({useScroll: false})

#### touchOpenReplaceTab ####

*Default* `false`   
*Expects* `boolean`

If you would like the image to replace the current window you are on when zooming set this to true. The user then can navigate back to the site using the back button which is simpler than closing the tab.

	$(selector).remooz({touchOpenReplaceTab: false})

#### viewNext ####

*Default* `false`   
*Expects* `selector`

Click on the zoomed image container to view the next image in the series.

	$(selector).remooz({viewNext: false})

#### showThumbs ####

*Default* `false`   
*Expects* `boolean`

Adds thumbnails into zoom container as well. This uses the same thumbnail images as found on the page.

	$(selector).remooz({showThumbs: false})

#### single ####

*Default* `false`   
*Expects* `selector, false`

Specifies that the image being clicked is a stand alone picture and is a part of a larger series. The selector refers to the other pictures in the same series.

	$(selector).remooz({single: false})

#### zoomTrigger ####

*Default* `false`   
*Expects* `selector, false`

Useful when there is a zoom trigger (zoom when clicking "this" icon) instead of clicking on the picture. Often used often in conjunction with mgBehaviour.

	$(selector).remooz({zoomTrigger: false})

#### imgOffset ####

*Default* `[0, 0, 0, 0]`   
*Expects* `top right bottom left`

Specifies the offset of the zoomed image. Required when the image needs to take into account padding and borders.

	$(selector).remooz({imgOffset: [0, 0, 0, 0]})

#### mgBehaviour ####

*Default* `fixed`   
*Expects* `fixed, fixed all, none`

This property handles how the zoom frame acts when the cursor reaches the each of the picture.
*	`fixed` frame is fixed at the border but the image moves inside frame.
*	`fixed all` fixes frame and disappears att edges if frame disappears.
*	`none` removes magnifying glass. Also if the class zoomMG is not found mgBehaviour defaults to none.

		

		$(selector).remooz({mgBehaviour: fixed})

#### mgImgOffset ####

*Default* `[0, 0, 0, 0]`   
*Expects* `top right bottom left`

Specifies offsets for the magnifying glass to take into account padding and borders.

	$(selector).remooz({mgImgOffset: [0, 0, 0, 0]})

#### debug ####

*Default* `false`   
*Expects* `boolean`

Helpful to get some debugging data. This should be off for production, prints object data straight to the console.

	$(selector).remooz({debug: false});


### Events ###

#### remooz.zoomOpened ####

Triggers when zoom popup has been opened.

	$(selector).on('remooz.zoomOpened', function(){ });


#### remooz.zoomClosed ####

Triggers when zoom popup has been closed.

	$(selector).on('remooz.zoomClosed', function(){ });


#### Classes ####

#### zoomImg ####

Can be set to a class or the keyword `currentTarget` to trigger the image that is hovered upon.

Numerous classes can be reassigned. Check the `defaultOpts {}` as to which classes are able to be manipulated.

	zoomCont: '#js-remooz-zoomContainer',
	zoomThumbCont: '#js-remooz-zoomThumbnailContainer',
	zoomPool: '#js-remooz-imagePool',
	zoomThumbPool: '#js-remooz-thumbnailPool',
	zoomMG: '#js-remooz-zoomMagnifyingGlass',
	zoomImg: 'img.current',
	close: '.js-remooz-close',
	prev: '.js-remooz-prev',
	next: '.js-remooz-next',
	preloader: '.js-remooz-preloader',
	skipSlide: 'redils-duplicated',


### Changelog ###

**Version 2.1.0**  
Added support for video.

**Version 2.0.0**  
Moved to new repository. [Old repo can be found here.](https://github.com/youngskilled/js-remooz) Made NPM compatible.

**Version 1.9.0**  
zoomImg now takes a keyword for when the zoom function should just take the image that is currently being targeted. Useful if all images are visible. Also fixed is a bug for top when scroll enabled. Css is now set to `top: 0`.

**Version 1.8.1**  
Added a property to control image movement when in zoom mode, now possible to scroll. Added a property to allow image to be opened in the same window. It is a window.location so for the user to get back to the current screen must navigate back. Changed the touch to be more sensitive now movement must be less than 40px.

**Version 1.8.0**  
Added events to when zoom is showing/hidden. Fixed index behaviour when changing images if images are not siblings to each other. Added imageOffset to images that are larger than the screen. Useful for fixed headers above zoom etc. Updated CSS to not include @extends buts to use a common class for all controls.

**Version 1.7.1**  
Added class to enable one to skip certain slides in slideshow mode. Default skips duplicated slides in redils slider.

**Version 1.7.0**  
Changed naming on all elements to be more BEM like. Not compatible with previous versions.

**Version 1.6.2**  
Added unminified plugin version

**Version 1.6.1**  
Updated jQuery dependency to be more accurate

**Version 1.5.3**  
Removed arrows in the zoom container if there is only one picture zoomed.

**Version 1.5.2**  
Tidied up styling of zoom.

**Version 1.5.1**  
Removed magnifying touch.

**Version 1.5**  
Made a major improvement on touch registering. No longer running on time but based on distance of finger moved.

**Version 1.4.2**  
Removed preventDefault on key presses. Inteferring with the global window object.

**Version 1.4.1**  
Stopped images from loading in on hover if single is chosen.
Remembers scroll position before loading image and returns user to that position on close.
Moved a preventDefault so that you can scroll on the page and adjusted the click time.

**Version 1.4**  
Added a preloader to enable a smoother transition between images.

**Version 1.3.4**  
Added a debug message when img.current not found.

**Version 1.3.3**  
On clicking of external zoom link image was not able to be found. Using parent then finding zoomImg from there. Allows zoom to be a sibling of the images.
Fixed ids for pictures that don't have a normal img suffix.

**Version 1.3.2**  
Fixed thumbnail clicking. Switch statement in changeZoomedImage not picking up the number.
Removed z-index from being fired every time mouse was moved in zoom mode.
Changed zoom id so that it is truly unique to every picture. Now uses the Image source tag to seperate between images.

**Version 1.3.1**  
Fixed a bug where no width or height was being set to the zoomed image, resulting in no image showing.

**Version 1.3**  
Refactored code to remove nested functions and removed repitition
Made offsets for magnifying glass and zoom to the same format.
Image size data is now retrieved from the image itself instead of relying on hand coded data-zoom tags.

**Version 1.2**  
Initiated events in remooz.init instead of inside a private function

### Development ###

**Requirements**
* This plugin requires [node](http://nodejs.org/), [gulpjs](http://gulpjs.com/) and [bower](http://bower.io/).
* Follow JSCS guidelines a styling-example.js is also included.
* Run `bower install` and `npm install` to get dev dependencies. Bower and Gulp is assumed to be running globally.

### Contact ###

This is a small plugin by Young Skilled.
Contact [richard](mailto:richard@coalescecreate.com) for more details about this plugin.
