# PLUGIN_NAME.printTable()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [PLUGIN_NAME.*](Readme.markdown)
| __Return value__     | None
| __Keywords__         | json
| __See also__         | 


## Overview

This function recursively prints the contents of a table to the console.


## Syntax

	PLUGIN_NAME.printTable( t )
	PLUGIN_NAME.printTable( t, label )
	PLUGIN_NAME.printTable( t, label, indentLevel )

##### t <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._ The Lua table you want to print to console.

##### label <small>(optional)</small>
_[String](http://docs.coronalabs.com/api/type/String.html)._ An optional string to be printed on its own line, before the contents of the table are printed. If nil or none provided, then no line is printed.

##### indentLevel <small>(optional)</small>
_[Number](http://docs.coronalabs.com/api/type/Number.html)._ The number of tabs indented before each line. Default is 0.


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

PLUGIN_NAME.printTable( colors )
``````
