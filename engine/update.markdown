# Engine.update()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine.*](type_engine.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function is currently unused and currently does nothing useful.

**NOTE: This function should not be used in the current version.**


## Syntax

``````lua
Engine.update( timeDelta )
``````

##### timeDelta <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The time passed in milliseconds since the last update call.

## Examples

``````lua
engineInstance.update( 1000 / 60 )
``````