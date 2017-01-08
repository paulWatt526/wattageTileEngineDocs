# Module.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Module.*](type_module.markdown)
| __Return value__     | [Module](type_module)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of type Module.


## Syntax

	Module.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### name <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
Name of the module.

##### rows <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Number of rows in the module.

##### columns <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Number of columns in the module.

##### lightingModel <small>(required)</small>
_[LightingModel](../lightingModel/type_lightingModel.markdown)._
LightingModel for the module.

##### losModel <small>(required)</small>
_[LineOfSightModel](../lineOfSightModel/type_lineOfSightModel.markdown)._
LineOfSightModel for the module.


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

-- Callback to indicate whether a tile is transparent
local function isTransparent(column, row)
    -- Make an opaque wall along column 5
    return column ~= 5
end

-- Callback to indicate whether a tile is affected by ambient lighting.
local function isTileAffectedByAmbient(row, column)
    -- Make all tiles affected by ambient lighting
    return true
end

local lightingModel = TileEngine.LightingModel.new({
    isTransparent = isTransparent,
    isTileAffectedByAmbient = isTileAffectedByAmbient,
    useTransitioners = true
})

local lineOfSightModel = TileEngine.LineOfSightModel.new({
    radius = 15,
    isTransparent = isTransparent
})

local myModule = TileEngine.Module.new({
    name = "myModule",
    rows = 100,
    columns = 100,
    lightingModel = lightingModel,
    losModel = lineOfSightModel
})
``````
