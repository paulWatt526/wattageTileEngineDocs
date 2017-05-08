# RegionManager.getEntityLocation()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.RegionManager.*](type_regionManager.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html), [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         |
| __See also__         |


## Overview

This function will return the X and Y coordinates of the entity in
world space.

**NOTE: This function should always be used when utilizing the
RegionManager.  Getting the x and y values directly
from the sprite will not factor in the local to world coordinate
conversions.**

## Syntax

	RegionManager.getEntityLocation( entityLayerIndex, entityId )

##### entityLayerIndex <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The index of the entity layer that contains the entity ID.

##### entityId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the entity to get the position of.

## Examples

``````lua
local x, y = regionManager.getEntityLocation(2, 42)
``````
