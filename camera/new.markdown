# Camera.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Camera](type_camera.markdown)
| __Return value__     | [Camera](type_camera.markdown)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of Camera.

**NOTE: This should never be necessary as an instance may be retrieved
from the ViewControl.**


## Syntax

	Camera.new( ARG1 )

##### ARG1 <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `ARG1` table contains the following properties:

##### x <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ X position of camera in tile units.  Values increase from
left to right.

##### y <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Y position of camera in tile units.  Values increase from
top to bottom.

##### width <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Width of the viewport in tile units.

##### height <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Height of the viewport in tile units.

##### pixelWidth <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Width of the viewport in pixels.

##### pixelHeight <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._ Height of the viewport in pixels.


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

local TILE_SIZE = 32
local CONTROL_WIDTH_IN_PIXELS = 320
local CONTROL_HEIGHT_IN_PIXELS = 256

local camera = TileEngine.Camera.new({
    x = 0,
    y = 0,
    width = CONTROL_WIDTH_IN_PIXELS / TILE_SIZE,
    height = CONTROL_HEIGHT_IN_PIXELS / TILE_SIZE,
    pixelWidth = CONTROL_WIDTH_IN_PIXELS,
    pixelHeight = CONTROL_HEIGHT_IN_PIXELS,
    layer = 1
})
``````
