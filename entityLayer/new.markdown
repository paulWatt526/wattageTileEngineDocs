# EntityLayer.new()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer](type_entityLayer.markdown)
| __Return value__     | [EntityLayer](type_entityLayer.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function creates a new instance of EntityLayer.


## Syntax

	EntityLayer.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### tileSize <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The size of the tiles used by the engine.  It is assumed that tiles
are square.

##### spriteResolver <small>(required)</small>
_[SpriteResolver](../spriteResolver/type_spriteResolver.markdown)._
The sprite resolver that the layer will use to resolve the keys
passed into the addEntity() function.


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

local spriteResolver = {}
spriteResolver.resolveForKey = function(key)
    return TileEngine.SpriteInfo.new({
        imageRect = display.newImageRect(key, 32, 32),
        width = 32,
        height = 32
    })
end

local entityLayer = TileEngine.EntityLayer.new({
    tileSize=32,
    spriteResolver=spriteResolver
})
``````
