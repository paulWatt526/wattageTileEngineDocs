# LineOfSightModel.ALL_VISIBLE

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Library__          | [wattageTileEngine.LineOfSightModel.*](type_lineOfSight.markdown)
| __Keywords__         |
| __See also__         | 


## Overview

This property is an implementation of the line of sight model which
will indicate that everything is visible.  This can be used when line of
sight is not something needed in the application.


## Example
 
``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local allVisible = TileEngine.LineOfSightModel.ALL_VISIBLE
``````
