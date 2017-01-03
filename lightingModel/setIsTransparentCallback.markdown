# LightingModel.setIsTransparentCallback()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function sets the callback function to be used to determine whether
a tile is transparent to light.


## Syntax

	LightingModel.setIsTransparentCallback( callback )

##### callback <small>(required)</small>
_[function](http://docs.coronalabs.com/api/type/Function.html)._
Sets the callback function used to determine whether a tile is
transparent to light.

The function should have the following signature:

    boolean function(column, row)


## Examples

``````lua
lightingModelInstance.setIsTransparentCallback(function (row, column)
  -- Make all tiles transparent
  return true
end)
``````
