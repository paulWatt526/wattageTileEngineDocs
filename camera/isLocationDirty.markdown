# Camera.isLocationDirty()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | [boolean](https://docs.coronalabs.com/api/type/Boolean.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns true if the camera has been moved since
the previous render call.  This is used internally by the engine.


## Syntax

	Camera.isLocationDirty()

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
local cameraMoved = camera.isLocationDirty()
``````
