# LightingModel.getLightProperties()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns the row, column, red, green, blue, intensity, and
radius values of the light with the specified id.  If no light with the
specified ID exists, nil is returned.


## Syntax

	LightingModel.getLightProperties( lightId )

##### lightId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the light for which info will be retrieved.


## Examples

``````lua
local light = lightingModelInstance.getLightPropertied(42)
local row = light.row
local column = light.column
local red = light.r
local green = light.g
local blue = light.b
local intensity = light.intensity
local radius = light.radius
``````
