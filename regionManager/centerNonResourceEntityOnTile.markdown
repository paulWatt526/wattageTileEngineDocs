# RegionManager.centerNonResourceEntityOnTile()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.RegionManager.*](type_regionManager.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will center a non-resource entity on the specified tile.

**NOTE: This function should always be used when utilizing the
RegionManager.  The function on the EntityLayer with the same name
should not be used as it does not handle the world and local coordinate
systems like this function does.**

## Syntax

	RegionManager.centerNonResourceEntityOnTile( entityLayerIndex, nonResourceEntityId, worldRow, worldColumn )

##### entityLayerIndex <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The index of the entity layer that contains the non-resource entity ID.

##### nonResourceEntityId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the non-resource entity to center on the tile.

##### worldRow <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row to center the non-resource entity on.  This coordinate is in world coordinates
not local layer coordinates.

##### worldColumn <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column to center the non-resource entity on.  This coordinate is in world coordinates
not local layer coordinates.

## Examples

``````lua
regionManager.centerNonResourceEntityOnTile(2, 42, 1, 1)
``````
