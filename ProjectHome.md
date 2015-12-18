Note: https://github.com/furf/jquery-ui-touch-punch may be a better solution however I have not tested.

Provides an interface layer to map touch events to jQuery UI interface elements.

Adds support for

  * Clicking = tap
  * Double Clicking = double tap
  * Dragging = touch and move
  * Right Click = touch and hold

It is completely unobtrusive (by using feature detection) and can be added to any jQuery UI project to provide support for apples mobile devices.


As per the issues this code does prevent default behavior such as pinch to zoom.
To avoid that issue, you can apply the changes directly to the jQuery UI elements in question. (I didn't need zoom or multi-touch features in the project this was written for)

Make the following changes: (thanks to Matt Motherway and [issue #5](https://code.google.com/p/jquery-ui-for-ipad-and-iphone/issues/detail?id=#5))


```
$.extend($.support, {
	touch: "ontouchend" in document
});

//
// Hook up touch events
//
$.fn.addTouch = function() {
	if ($.support.touch) {
		this.each(function(i,el){
			el.addEventListener("touchstart", iPadTouchHandler, false);
			el.addEventListener("touchmove", iPadTouchHandler, false);
			el.addEventListener("touchend", iPadTouchHandler, false);
			el.addEventListener("touchcancel", iPadTouchHandler, false);
		});
	}
};

var lastTap = null;	
....
```

Then call addTouch on the elements with jQuery UI functions applied:

```
$('Element').dialog().addTouch();
```