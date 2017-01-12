# LightingModel.markChangeInTransparency()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel.*](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function informs the lighting model of a change in transparency.
This may occur by dynamically adding or removing a wall for example.
The should be called when transparencies change on tiles.


## Syntax

	LightingModel.markChangeInTransparency( row, col )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Row of the tile.

##### col <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Column of the tile.


## Examples

``````lua
lightingModelInstance.markChangeInTransparency(10, 15)
``````
