# Camera.isLayerDirty()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | [boolean](https://docs.coronalabs.com/api/type/Boolean.html)
| __Keywords__         | 
| __See also__         | 


## Overview

This function returns true if the value of layer has been altered since
the previous render call.  This is used internally by the engine.


## Syntax

	Camera.isLayerDirty()

## Examples

``````lua
-- tileEngineViewControl is an instance of ViewControl
local camera = tileEngineViewControl.getCamera()
local layerChanged = camera.isLayerDirty()
``````
