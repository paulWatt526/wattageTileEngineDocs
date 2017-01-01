# Camera.setZoom()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | VOID
| __Keywords__         | Wattage, Layer, TileLayer, EntityLayer
| __See also__         |


## Overview

This function sets the zoom of the camera.  A zoom of one indicates no
zoom.

**NOTE: The zoom should be set before the first render and not changed
afterwards.  Dynamically changing the zoom may result in unwanted
artifacts.  This may be addressed in a future build.**

## Syntax

	Camera.setZoom( ARG1 )

##### ARG1 <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ The zoom
value to apply to the camera.  A value of 1 indicates no zoom, values
less than 1 but greater than 0 results in zooming out, and values greater
than 1 results in zooming in.

**NOTE: Values should be greater than 0.**

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()

-- zoom in to double size.
camera.setZoom(2.0)
``````
