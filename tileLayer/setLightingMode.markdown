# TileLayer.setLightingMode()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.TileLayer.*](type_tileLayer.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will set the the lighting mode for this layer.  The two
modes available are:

* Ambient Only - Only ambient lighting applies to this layer.
* All - All lighting applies to this layer.
* None - No lighting is applied to this layer.  The sprites
are drawn "as is".

There are constants defined for the modes:

``````lua
local TileEngine = require "plugin.wattageTileEngine"

TileEngine.LayerConstants.LIGHTING_MODE_APPLY_ALL
TileEngine.LayerConstants.LIGHTING_MODE_AMBIENT_ONLY
TileEngine.LayerConstants.LIGHTING_MODE_NONE
``````

The default mode is LIGHTING_MODE_APPLY_ALL.

## Syntax

	TileLayer.setLightingMode( mode )

##### mode <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The lighting mode for the layer.

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

tileLayerInstance.setLightingMode(TileEngine.LayerConstants.LIGHTING_MODE_AMBIENT_ONLY)
``````
