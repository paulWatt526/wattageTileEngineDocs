# Camera

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Camera](type_camera.markdown)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Keywords__         | Wattage, Camera, Tile Engine
| __See also__         |

## Overview

A camera is used by the tile engine renderer to determine what is
visible.  In typical usage, the camera will be created by the ViewControl
and not the developer.

## Syntax

An instance of the camera can be retrieved from the ViewControl.

	-- tileEngineViewControl is an instance of ViewControl
	local camera = tileEngineViewControl.getCamera()

	-- set camera location in tile coordinates (not pixels)
	camera.setLocation(10.5, 10.5)

	-- pass camera to the tile engine's render function
	tileEngine.render(camera)

### Constructor

#### [new()](new.markdown)

### Functions

##### [isLocationDirty()](isLocationDirty.markdown)

##### [setLocationDirty()](setLocationDirty.markdown)

##### [setLocation()](setLocation.markdown)

##### [getX()](getX.markdown)

##### [getY()](getY.markdown)

##### [getLayer()](getLayer.markdown)

##### [setLayer()](setLayer.markdown)

##### [isLayerDirty()](isLayerDirty.markdown)

##### [setLayerDirty()](setLayerDirty.markdown)

##### [getZoom()](getZoom.markdown)

##### [setZoom()](setZoom.markdown)

##### [isZoomDirty()](isZoomDirty.markdown)

##### [setZoomDirty()](setZoomDirty.markdown)


### Properties

##### [width](width.markdown)

##### [height](height.markdown)

##### [pixelWidth](pixelWidth.markdown)

##### [pixelHeight](pixelHeight.markdown)
