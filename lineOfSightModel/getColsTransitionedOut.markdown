# LineOfSightModel.getColsTransitionedOut()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSight](type_lineOfSight.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns a table containing the column component of all
tiles transitioned out of line of sight.  The order of this list matches
that of getRowsTransitionedOut().  So the value at the same index from each
gives the complete row, column coordinate.


## Syntax

	LineOfSightModel.getColsTransitionedOut()


## Examples

``````lua
local outRows = lineOfSightModelInstance.getRowsTransitionedOut()
local outCols = lineOfSightModelInstance.getColsTransitionedOut()

local outTileCoords = {}
for i=1,#outRows do
    local row = outRows[i]
    local col = outCols[i]
    table.insert(outTileCoords, {row = row, col = col})
end
``````
