# Utils.loadJsonFile()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Utils.*](lib_utils.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | 
| __See also__         | 


## Overview

This function loads contents of a JSON file into a table.


## Syntax

	Utils.loadJsonFile( fileName )

##### fileName <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
The name of the file to load the table from.


## Examples

``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local Utils = TileEngine.Utils

local loadedTable = Utils.loadJsonFile("json.dat")
``````
