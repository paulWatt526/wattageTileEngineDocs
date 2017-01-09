# LightingModel.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel.*](type_lightingModel.markdown)
| __Return value__     | [LightingModel](type_lightingModel.markdown)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of LightingModel.


## Syntax

	LightingModel.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### isTransparent <small>(required)</small>
_[function](http://docs.coronalabs.com/api/type/Function.html)._
Callback which returns true if the tile is transparent.  The callback
must have the following signature:

    boolean function(column, row)


##### isTileAffectedByAmbient <small>(required)</small>
_[function](http://docs.coronalabs.com/api/type/Function.html)._
Callback which returns true if the tile is affected by ambient lighting.
The callback must have the following signature:

    boolean function(column, row)

##### useTransitioners <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._
True if the changes in lighting should transition smoothly.  Setting
this to false will result in lighting conditions changing immediately.
Setting to true will apply the changes gradually over 250 milliseconds.

##### compensateLightingForViewingPosition <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._
This must be set to true if the engine also has it set to true.  However,
doing so does require additional overhead which can affect performance.


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

-- Callback to indicate whether light can pass through a tile
local function isTransparentForLight(column, row)
    -- Make an opaque wall along column 5
    return column ~= 5
end

-- Callback to indicate whether a tile is affected by ambient lighting.
local function isTileAffectedByAmbient(row, column)
    -- Make all tiles affected by ambient lighting
    return true
end

local lightingModel = TileEngine.LightingModel.new({
    isTransparent = isTransparentForLight,
    isTileAffectedByAmbient = isTileAffectedByAmbient,
    useTransitioners = true,
    compensateLightingForViewingPosition = false
})
``````
