# LineOfSightModel.new()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSightModel](type_lineOfSightModel.markdown)
| __Return value__     | [LineOfSightModel](type_lineOfSightModel.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function creates a new instance of LineOfSightModel.


## Syntax

	LineOfSightModel.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### radius <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Maximum radius of the line of sight.

##### isTransparent <small>(required)</small>
_[function](http://docs.coronalabs.com/api/type/Function.html)._
Callback which returns true if the tile is transparent.  The callback
must have the following signature:

    boolean function(column, row)


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

-- Callback to indicate whether line of sight can pass through tile
local function isTransparent(column, row)
    -- Make an opaque wall along column 5
    return column ~= 5
end

local lineOfSightModel = TileEngine.LineOfSightModel.new({
    radius = 15,
    isTransparent = isTransparent
})
``````
