# Utils.getFromGrid()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Utils.*](lib_utils.markdown)
| __Return value__     | Value
| __Keywords__         |
| __See also__         |


## Overview

This function retrieves a value from a grid at the specified row and
column or nil if no value exists there.


## Syntax

	Utils.getFromGrid( grid, row, column )

##### grid <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
The table in which the value will be inserted.

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row to get the value from.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column to get the value from.


## Examples

``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local Utils = TileEngine.Utils

local value = Utils.getFromGrid(grid, 10, 15)
``````