# LineOfSightModel.getCoordinatesIn()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSightModel.*](type_lineOfSight.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns a table containing the tiles currently in the
line of sight.


## Syntax

	LineOfSightModel.getCoordinatesIn()


## Examples

``````lua
local inRowColumnPairs = {}
local coordsIn = lineOfSightModelInstance.getCoordinatesIn()
for row, columns in pairs(coordsIn) do
    for col, tile in pairs(columns) do
        table.insert(inRowColumnPairs, {row = row, col = col})
    end
end
``````
