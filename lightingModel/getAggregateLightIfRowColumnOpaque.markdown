# LightingModel.getAggregateLightIfRowColumnOpaque()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns the aggregated red, green, and blue values of all
the lights which affect an opaque tile.  The location of the viewer is
taken into account.  If the specified row and column is not opaque, then
nil is returned.


## Syntax

	LightingModel.getAggregateLightIfRowColumnOpaque( row, col, viewRow, viewCol )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Row of the tile.

##### col <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Column of the tile.

##### viewRow <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Row of the view point.

##### viewCol <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Column of the view point.


## Examples

``````lua
local light = lightingModelInstance.getAggregateLightIfRowColumnOpaque(10, 15, 12, 17)
local red = light.r
local green = light.g
local blud = light.b
``````
