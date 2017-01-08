# Tile.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Tile.*](type_tile.markdown)
| __Return value__     | [Tile](type_tile)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of type Tile.


## Syntax

	Tile.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### resourceKey <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
The key that will be passed to the SpriteResolver.

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local Tile = TileEngine.Tile

local tileInstance = Tile.new({
    resourceKey = "tree"
})
``````