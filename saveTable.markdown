# PLUGIN_NAME.saveTable()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [PLUGIN_NAME.*](Readme.markdown)
| __Return value__     | [Boolean](http://docs.coronalabs.com/api/type/Boolean.html)
| __Keywords__         | json
| __See also__         | [PLUGIN_NAME.loadTable()](loadTable.markdown)


## Overview

This function saves a Lua table to a JSON file


## Syntax

	PLUGIN_NAME.saveTable( t, filename )
	PLUGIN_NAME.saveTable( t, filename, baseDirectory )

##### t <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._ The Lua table you want to persist to a file.

##### filename <small>(required)</small>
_[String](http://docs.coronalabs.com/api/type/String.html)._ The name of the file that will contain the JSON data.

##### baseDirectory <small>(optional)</small>
_[Constant](http://docs.coronalabs.com/api/type/Constant.html)._ Constant corresponding to the base directory where the file is located. Default value is [system.DocumentsDirectory](http://docs.coronalabs.com/api/library/system/DocumentsDirectory.html) if the parameter is not provided.


## Examples

``````lua
local PLUGIN_NAME = require 'plugin.PLUGIN_NAME'

local colors = 
{
	{ name = "red",		value = { 1, 0, 0, 1 }, },
	{ name = "green",	value = { 0, 1, 0, 1 }, },
	{ name = "blue",	value = { 0, 0, 1, 1 }, },
	{ name = "cyan",	value = { 0, 1, 1, 1 }, },
	{ name = "magenta",	value = { 1, 0, 1, 1 }, },
	{ name = "yellow",	value = { 1, 1, 0, 1 }, },
}

PLUGIN_NAME.saveTable( colors, "colors.json" )
``````
