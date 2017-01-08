# LineOfSightModel.isInLineOfSight()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LineOfSightModel.*](type_lineOfSightModel.markdown)
| __Return value__     | [boolean](https://docs.coronalabs.com/api/type/Boolean.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns if the tile is currently in the line of sight,
otherwise false.


## Syntax

	LineOfSightModel.isInLineOfSight( row, column )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row of the tile.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the tile.


## Examples

``````lua
local isInLOS = lineOfSightModelInstance.isInLineOfSight(10, 15)
``````
