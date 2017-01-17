# TileLayer.getLightingMode()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.TileLayer.*](type_tileLayer.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html)
| __Keywords__         |
| __See also__         |


## Overview

This function will get the the lighting mode for this layer.  The two
modes available are:

* Ambient Only - Only ambient lighting applies to this layer.
* All - All lighting applies to this layer.

There are constants defined for the modes:

``````lua
local TileEngine = require "plugin.wattageTileEngine"

TileEngine.LayerConstants.LIGHTING_MODE_APPLY_ALL
TileEngine.LayerConstants.LIGHTING_MODE_AMBIENT_ONLY
``````

The default mode is LIGHTING_MODE_APPLY_ALL.

## Syntax

	TileLayer.getLightingMode()

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

local mode = tileLayerInstance.getLightingMode()
``````