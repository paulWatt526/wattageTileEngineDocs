# Camera.getLayer()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera.*](type_camera.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         | Wattage, Layer, TileLayer, EntityLayer
| __See also__         | 


## Overview

This function returns the index of the layer which the camera is currently
focused on.  The layer which the camera is focused on will have a scaling
factor of one.

## Syntax

	Camera.getLayer()

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
local curLayerIndex = camera.getLayer()
``````
