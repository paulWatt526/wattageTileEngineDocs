# SpriteInfo.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.SpriteInfo.*](type_spriteInfo.markdown)
| __Return value__     | [SpriteInfo](type_spriteInfo)
| __Keywords__         | 
| __See also__         | 


## Overview

***NOTE: THIS FUNCTION IS DEPRECATED.  IN ITS PLACE SIMPLY USE A TABLE
WITH THE PROPERTIES: imageRect, width, and height.  FOR EXAMPLE:***

``````lua
local displayObject = display.newImageRect("img/myImage.png", 100, 100)
local spriteInfo = {
    imageRect = displayObject,
    width = 100,
    height = 100
}
``````

***REPEATEDLY CALLING SpriteInfo.new() HAS A SLIGHT PERFORMANCE IMPACT.***


This function creates a new instance of type SpriteInfo.

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