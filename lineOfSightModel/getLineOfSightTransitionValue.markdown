# LineOfSightModel.getLineOfSightTransitionValue()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns the value of a tile even when in transition.  The
returned value will be 0 for not in line of sight and 1 for in line
of sight.  A fractional value represents a transition from one state to
another.


## Syntax

	LineOfSightModel.getLineOfSightTransitionValue( row, column )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row of the tile to get the transition value from.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the tile to get the transition value from.


## Examples

``````lua
local value = lineOfSightModelInstance.getLineOfSightTransitionValue(10, 15)
``````
