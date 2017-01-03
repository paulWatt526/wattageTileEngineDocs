# LightingModel.update()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function updates the lighting model.  This will result in handling
any dirty lighting information as well as advancing any transitions
between lighting states.


## Syntax

``````lua
LightingModel.update( timeDelta )
``````

##### timeDelta <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The time passed in milliseconds since the last update call.

## Examples

``````lua
lightingModelInstance.update( 1000 / 60 )
``````