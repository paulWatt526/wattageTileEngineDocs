# LightingModel.resetDirtyFlags()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.LightingModel.*](type_lightingModel.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function resets all of the tracking of dirty data in the engine.

**NOTE: This should be called after the update function in every frame.**

## Syntax

	LightingModel.resetDirtyFlags()


## Examples

``````lua
lightingModelInstance.resetDirtyFlags()
``````
