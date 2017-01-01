# Camera.setLayer()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | VOID
| __Keywords__         | Wattage, Layer, TileLayer, EntityLayer
| __See also__         |


## Overview

This function sets the index of the layer which the camera will
focus on.  The layer which the camera is focused on will have a scaling
factor of one.

## Syntax

	Camera.setLayer( ARG1 )

##### ARG1 <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ The index
of the layer that the camera will focus on.  This results in the
specified layer having a scaling value of 1 and is useful when
parallax is being used with multiple layers.

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
camera.setLayer(3)
``````
