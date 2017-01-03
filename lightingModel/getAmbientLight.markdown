# LightingModel.getAmbientLight()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns the red, green, blue, and intensity values of the
ambient light.


## Syntax

	LightingModel.getAmbientLight()


## Examples

``````lua
local light = lightingModelInstance.getAmbientLight()
local red = light.r
local green = light.g
local blud = light.b
local intensity = light.intensity
``````