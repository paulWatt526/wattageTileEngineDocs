# LightingModel.getDirtyAggregateRows()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel.*](type_lightingModel.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns a table containing the row component of all
dirty tiles.  The order of this list matches that of
getDirtyAggregateColumns().  So the value at the same index from each
gives the complete row, column coordinate of a dirty tile.


## Syntax

	LightingModel.getDirtyAggregateRows()


## Examples

``````lua
local dirtyRows = lightingModelInstance.getDirtyAggregateRows()
local dirtyCols = lightingModelInstance.getDirtyAggregateColumns()

local dirtyTileCoords = {}
for i=1,#dirtyRows do
    local row = dirtyRows[i]
    local col = dirtyCols[i]
    table.insert(dirtyTileCoords, {row = row, col = col})
end
``````
