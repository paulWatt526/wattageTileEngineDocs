# RegionManager.setCameraLocation()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.RegionManager.*](type_regionManager.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will set the location of the camera.

**NOTE: This function should always be used to set the camera's location
when utilizing the RegionManager.  Setting the position directly
on the camera will not factor in the world to local coordinate
conversions.**

## Syntax

	RegionManager.setCameraLocation( worldX, worldY )

##### worldX <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The X position of the camera in world coordinates.  These values are
in tile units.

##### worldY <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The Y position of the camera in world coordinates.  These values are
in tile units.

## Examples

``````lua
regionManager.setCameraLocation(10.5, 5.5)
``````
