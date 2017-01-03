# LightingModel.getAggregateLight()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         | 
| __See also__         | 


## Overview

This function returns the aggregated red, green, and blue values of all
the lights which affect the tile.


## Syntax

	LightingModel.getAggregateLight( row, col )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Row of the tile.

##### col <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Column of the tile.


## Examples

``````lua
local light = lightingModelInstance.getAggregateLight(10, 15)
local red = light.r
local green = light.g
local blud = light.b
``````
