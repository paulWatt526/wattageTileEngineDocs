# Utils.addToGrid()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Utils.*](lib_utils.markdown)
| __Return value__     | VOID
| __Keywords__         | 
| __See also__         | 


## Overview

This function adds a value to a grid at the specified row and
column.


## Syntax

	Utils.addToGrid( value, grid, row, column )

##### value <small>(required)</small>
_Value._ The value to store at the row and column in the grid.

##### grid <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
The table in which the value will be inserted.

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row to insert the value in.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column to insert the value in.


## Examples

``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local Utils = TileEngine.Utils

local grid = {}
Utils.addToGrid("value at (10, 15)", grid, 10, 15)
``````