# LightingModel.setIsTileAffectedByAmbientCallback()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function sets the callback function used to determine whether a tile
should be affected by ambient light.


## Syntax

	LightingModel.setIsTileAffectedByAmbientCallback( callback )

##### callback <small>(required)</small>
_[function](http://docs.coronalabs.com/api/type/Function.html)._
The callback function used to determine whether a tile should be
affected by ambient light.

The function should have the following signature:

    boolean function(column, row)


## Examples

``````lua
lightingModelInstance.setIsTileAffectedByAmbientCallback(function (row, column)
  -- Make all tiles affected by ambient lighting
  return true
end)
``````
