# EntityLayer.setEntityTilePosition()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer.*](type_entityLayer.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will set the position of an entity using row and column
coordinates.

Note that the values for row and column are continuous and thus can
represent a position between tiles.  The center of the tile at
row 1 and column 4 would be row 0.5 and column 3.5.


## Syntax

	EntityLayer.setEntityTilePosition( id, row, column )

##### id <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the entity.

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row to move the entity to.

Note that the values for row and column are continuous and thus can
represent a position between tiles.  The center of the tile at
row 1 and column 4 would be row 0.5 and column 3.5.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column to move the entity to.

Note that the values for row and column are continuous and thus can
represent a position between tiles.  The center of the tile at
row 1 and column 4 would be row 0.5 and column 3.5.

## Examples

``````lua
entityLayerInstance.setEntityTilePosition(42, 10, 15)
``````
