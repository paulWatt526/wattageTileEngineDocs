# PLUGIN_NAME.loadTable()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [PLUGIN_NAME.*](Readme.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | json
| __See also__         | [PLUGIN_NAME.saveTable()](saveTable.markdown)


## Overview

This function loads a JSON file and returns a corresponding Lua table.


## Syntax

	PLUGIN_NAME.loadTable( filename )
	PLUGIN_NAME.loadTable( filename, baseDirectory )

##### filename <small>(required)</small>
_[String](http://docs.coronalabs.com/api/type/String.html)._ The name of the file that will contain the JSON data.

##### baseDirectory <small>(optional)</small>
_[Constant](http://docs.coronalabs.com/api/type/Constant.html)._ Constant corresponding to the base directory where the file is located. Default value is [system.DocumentsDirectory](http://docs.coronalabs.com/api/library/system/DocumentsDirectory.html) if the parameter is not provided.


## Examples

``````lua
local PLUGIN_NAME = require 'plugin.PLUGIN_NAME'

local colors = PLUGIN_NAME.loadTable( "colors.json" )
``````
