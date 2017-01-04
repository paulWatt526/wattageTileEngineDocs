# LineOfSightModel.getDirtyRows()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSight](type_lineOfSight.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns a table containing the row component of all
dirty tiles.  The order of this list matches that of
getDirtyColumns().  So the value at the same index from each
gives the complete row, column coordinate.


## Syntax

	LineOfSightModel.getDirtyRows()


## Examples

``````lua
local dirtyRows = lineOfSightModelInstance.getDirtyRows()
local dirtyCols = lineOfSightModelInstance.getDirtyColumns()

local dirtyTileCoords = {}
for i=1,#dirtyRows do
    local row = dirtyRows[i]
    local col = dirtyCols[i]
    table.insert(dirtyTileCoords, {row = row, col = col})
end
``````
