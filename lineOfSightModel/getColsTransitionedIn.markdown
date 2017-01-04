# LineOfSightModel.getColsTransitionedIn()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSight](type_lineOfSight.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | 
| __See also__         | 


## Overview

This function returns a table containing the column component of all
tiles transitioned into line of sight.  The order of this list matches
that of getRowsTransitionedIn().  So the value at the same index from each
gives the complete row, column coordinate.


## Syntax

	LineOfSightModel.getColsTransitionedIn()


## Examples

``````lua
local inRows = lineOfSightModelInstance.getRowsTransitionedIn()
local inCols = lineOfSightModelInstance.getColsTransitionedIn()

local inTileCoords = {}
for i=1,#inRows do
    local row = inRows[i]
    local col = inCols[i]
    table.insert(inTileCoords, {row = row, col = col})
end
``````
