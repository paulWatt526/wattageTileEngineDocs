# Utils.removeFromGrid()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Utils.*](lib_utils.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function removes a value from a grid at the specified row and
column.


## Syntax

	Utils.removeFromGrid( grid, row, column )

##### grid <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
The table from which the value will be removed.

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row to remove the value from.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column to remove the value from.


## Examples

``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local Utils = TileEngine.Utils

local grid = {}
Utils.removeFromGrid(grid, 10, 15)
``````