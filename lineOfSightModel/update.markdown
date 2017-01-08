# LineOfSightModel.update()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSightModel.*](type_lineOfSightModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function updates the line of sight model.  This will result in
advancing any tile transitions between line of sight status and will
recalculate using the supplied center tile coordinate if it was marked
as dirty since the last update.


## Syntax

``````lua
LineOfSightModel.update( centerRow, centerColumn, timeDelta )
``````

##### centerRow <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row of the center point of the line of sight.

##### centerColumn <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the center point of the line of sight.

##### timeDelta <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The time passed in milliseconds since the last update call.

## Examples

``````lua
lineOfSightModelInstance.update( 10, 15,  1000 / 60 )
``````