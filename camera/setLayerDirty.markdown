# Camera.setLayerDirty()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | VOID
| __Keywords__         | Wattage, Layer, TileLayer, EntityLayer
| __See also__         |


## Overview

This function sets the layer dirty flag.  This flag is used internally
by the engine to determine whether the camera's focus layer has changed
since the last rendering.

**NOTE: This function is used internally by the engine.**

## Syntax

	Camera.setLayerDirty( dirty )

##### dirty <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._ True
to indicate that the focus layer has been changed.

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
camera.setLayerDirty(true)
``````
