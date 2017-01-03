# Engine.isTileVisibleInLayer()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | [boolean](https://docs.coronalabs.com/api/type/Boolean.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns true if the tile at the specified coordinate is
visible to the camera.  This will factor in the scaling delta of the
specified layer and the zoom level of the camera when determining
visibility.


## Syntax

	Engine.isTileVisibleInLayer( layerIndex, row, column )

##### layerIndex <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
Index of the layer to check.

##### row <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The row of the tile to check.

##### column <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the tile to check.


## Examples

``````lua
local tileIsVisible = engineInstance.isTileVisibleInLayer( 1, 10, 15)
``````
