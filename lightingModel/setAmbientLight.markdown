# LightingModel.setAmbientLight()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function sets the values for ambient lighting.


## Syntax

	LightingModel.setAmbientLight( r, g, b, i )

##### r <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The red value of the light.  Number should be in range 0 to 1.

##### g <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The green value of the light.  Number should be in range 0 to 1.

##### b <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The blue value of the light.  Number should be in range 0 to 1.

##### intensity <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The intensity of the light. Number should be greater than or equal to
zero.  An intensity greater than one will be quite bright.


## Examples

``````lua
-- Set a medium intensity white ambient light
lightingModelInstance.setAmbientLight(1, 1, 1, 0.5)
``````
