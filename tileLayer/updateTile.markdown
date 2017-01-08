# TileLayer.updateTile()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will update the tile at the specified row and column.


## Syntax

	TileLayer.updateTile( row, column, newValue )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row of the tile to update.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the tile to update.

##### newValue <small>(required)</small>
_[Tile](../tile/type_tile.markdown)._
The new value for the tile at the specified row and column.

## Examples

``````lua
tileLayerInstance.updateTile(10, 15, Tile.new({
    resourceKey = "tree"
}))
``````