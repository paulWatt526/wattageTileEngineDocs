# RegionManager.setEntityLocation()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.RegionManager.*](type_regionManager.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will center the entity with the specified ID in the
specified entity layer on the specified point in world coordinates.

**NOTE: This function should always be used to set an entity's position
when utilizing the RegionManager.  Setting the x and y values directly
on the sprite will not factor in the world to local coordinate
conversions.**

## Syntax

	RegionManager.setEntityLocation( entityLayerIndex, entityId, worldX, worldY )

##### entityLayerIndex <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The index of the entity layer that contains the entity ID.

##### entityId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the entity to set the position of.

##### worldX <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The x coordinate to center the entity on.  This coordinate is in world coordinates
not local layer coordinates.

##### worldY <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The y coordinate to center the entity on.  This coordinate is in world coordinates
not local layer coordinates.

## Examples

``````lua
regionManager.setEntityLocation(2, 42, 1, 1)
``````
