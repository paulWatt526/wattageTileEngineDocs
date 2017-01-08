# Camera.setLocation()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera.*](type_camera.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function sets the location of the camera.


## Syntax

	Camera.setLocation( x, y )

##### x <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The X coordinate of the camera in tile units. (not pixels)

##### y <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The Y coordinate of the camera in tile units. (not pixels)


## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
camera.setLocation(2.5, 3.0)
``````
