# EntityLayer.centerNonResourceEntityOnTile()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer](type_entityLayer.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will center the entity associated with the specified ID
on the tile specified by the coordinates.


## Syntax

	EntityLayer.centerNonResourceEntityOnTile( id, row, column )

##### id <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the entity to center.

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
 The row of the tile to center the entity on.

 **NOTE: Row numbers start at 1 and increase from top to bottom.**

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the tile to center the entity on.

**NOTE: Column numbers start at 1 and increase from left to right.**

## Examples

``````lua
entityLayerInstance.centerNonResourceEntityOnTile(42, 10, 15)
``````
