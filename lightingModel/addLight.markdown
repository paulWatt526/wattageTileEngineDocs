# LightingModel.addLight()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         | 
| __See also__         | 


## Overview

This function adds a new light to the lighting model.  An ID will be
returned which can be used to access the light.

**NOTE: Lighting calculations can be expensive.  The cost of the
calculations increases exponentially with the radius of the light.  The
Wattage Tile Engine is optimized to make those calculations only when
necessary.  This means that lighting data is calculated only when a
change is detected and only for affected areas.  For static lighting,
this cost is incurred just once upon adding the light.  However, for
dynamic lighting, the cost is incurred any time the light is moved.
So care should be taken when deciding a radius for a dynamic light in
order to support higher frame rates.**


## Syntax

	LightingModel.addLight( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row to add the new light to.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column to add the new light to.

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

##### radius <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The maximum radius that the light will reach to.  The gradient of
intensity from the light to the outer radius will be impacted by the
specified intensity.

## Examples

``````lua
-- Add a yellow light
local lightId = lightingModelInstance.addLight({
    row = 10,
    column = 15,
    r = 1,
    g = 1,
    b = 0,
    intesity = 0.5,
    radius = 10
})
``````
