# Camera.getX()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         | Wattage, Camera
| __See also__         | 


## Overview

This function retrieves the current X position of the camera.  This
position is along the horizontal X-axis which increases in value from
left to right.

The unit of the returned value is tiles.  For example, given the
following...

* Each tile is 32x32 pixels
* The tile grid dimensions are 5x6.
* The origin is at the top left of the tile grid.
* The camera is pointing at the center of the grid.

...this function would return 2.5

NOTE: It would not return the pixel value of 80!


## Syntax

	Camera.getX()

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
local curX = camera.getX()
``````
