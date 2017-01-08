# SpriteInfo.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Return value__     | [SpriteInfo](type_spriteInfo)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of type SpriteInfo.

**NOTE: This function is called internally by the engine.**


## Syntax

	SpriteInfo.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### imageRect <small>(required)</small>
_[DisplayObject](https://docs.coronalabs.com/api/type/DisplayObject/index.html)._
The DisplayObject for the sprite.

##### width <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The width of the sprite.

##### height <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The height of the sprite.

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local SpriteInfo = TileEngine.SpriteInfo

local square = Display.newRect(10, 10, 10, 10)
local spriteInfoInstance = SpriteInfo.new({
    imageRect = square,
    width = 10,
    height = 10
})
``````