# Camera.getZoom()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera.*](type_camera.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         | Wattage, Camera
| __See also__         |


## Overview

This function retrieves the current zoom value of the camera.  No zoom
is indicated by the value 1.


## Syntax

	Camera.getZoom()

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
local curZoom = camera.getZoom()
``````
