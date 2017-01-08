# TileLayer.getDirtyTileCoordinates()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.*](Readme.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | 
| __See also__         | 


## Overview

This function retrieves the coordinates of dirty tiles in
the layer.


## Syntax

	TileLayer.getDirtyTileCoordinates()


## Examples

``````lua
local dirtyCoords = tileLayerInstance.getDirtyTileCoordinates()

print("Dirty Coordinates")
for i=1,#dirtyCoords do
    local coord = dirtyCoords[i]
    print("Row: " .. coord.row .. ", " .. "Column: " .. coord.column)
end
``````