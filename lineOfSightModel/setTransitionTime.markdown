# LineOfSightModel.setTransitionTime()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSightModel.*](type_lineOfSightModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will set the time transitions take to complete.  The value
is in milliseconds.


## Syntax

``````lua
LineOfSightModel.setTransitionTime( time )
``````

##### time <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The number of milliseconds for the transition.

## Examples

``````lua
lineOfSightModelInstance.setTransitionTime( 250 )
``````