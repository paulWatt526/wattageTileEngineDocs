# LightingModel.setUseTransitioners()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel.*](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function toggles whether or not changes in lighting will be
applied smoothly or instantly.


## Syntax

	LightingModel.setUseTransitioners( value )

##### value <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._
True to transition lighting changes smoothly, false to transition
lighting changes immediately.


## Examples

``````lua
-- Enable smooth lighting transitions
lightingModelInstance.setUseTransitioners(true)
``````
