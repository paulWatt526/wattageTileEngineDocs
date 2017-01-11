# EntityLayer.getEntityTilePosition()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer.*](type_entityLayer.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html), [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         |
| __See also__         |


## Overview

This function will return the position of the entity with the
specified ID.  The position is returned as row and column.

Note that the values for row and column are continuous and thus can
represent a position between tiles.  The center of the tile at
row 1 and column 4 would be row 0.5 and column 3.5.


## Syntax

	EntityLayer.getEntityTilePosition( id )

##### id <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the entity.

## Examples

``````lua
local row, col = entityLayerInstance.getEntityTilePosition(42)
``````
