# LightingModel.markLightAsDirtyIfAffectedAreaContainsTile()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel.*](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function marks any lights dirty which contain the specified
coordinate in their affected areas.  This is useful when dynamically
changing the opaqueness of tiles.


## Syntax

	LightingModel.markLightAsDirtyIfAffectedAreaContainsTile( row, col )

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Row of the tile.

##### col <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Column of the tile.


## Examples

``````lua
lightingModelInstance.markLightAsDirtyIfAffectedAreaContainsTile(10, 15)
``````
