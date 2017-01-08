# Camera.setZoomDirty()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera.*](type_camera.markdown)
| __Return value__     | VOID
| __Keywords__         | Wattage, Layer, TileLayer, EntityLayer
| __See also__         |


## Overview

This function sets the zoom dirty flag.  This flag is used internally
by the engine to determine whether the camera's zoom has changed
since the last rendering.

**NOTE: This function is used internally by the engine.**

## Syntax

	Camera.setZoomDirty( dirty )

##### dirty <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ True
to indicate that the camera's zoom has been changed.

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
camera.setZoomDirty(true)
``````
