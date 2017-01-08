# Engine.new()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine.*](type_[engine.markdown)
| __Return value__     | [Engine](type_engine.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function creates a new instance of Engine.


## Syntax

	Engine.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### parentGroup <small>(required)</small>
_[GroupObject](https://docs.coronalabs.com/api/type/GroupObject/index.html)._
All display objects managed by the engine will be children or
grandchildren of this group.

##### tileSize <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The size of the tiles used by the engine.  It is assumed that tiles
are square.

##### spriteResolver <small>(required)</small>
_[SpriteResolver](../spriteResolver/type_spriteResolver.markdown)._
The sprite resolver that the layer will use to resolve the keys
passed into the addEntity() function.

##### compensateLightingForViewingPosition <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._
There may be cases where the lighting applied to a tile depends on
the position of the viewer.  For example, a tile may represent the
outer wall of a building.  If the viewer is outside the building, it
should be lit brightly since it is daytime outside.  However, if the
viewer is inside the building, it should be lit dimly by an indoor
light or perhaps no light at all.  Setting this property to true
will result in the appropriate lighting according to the view position.
Setting this property to false will always use the aggregate lighting
of the tile.

##### hideOutOfSightElements <small>(required)</small>
_[boolean](https://docs.coronalabs.com/api/type/Boolean.html)._
Setting this value to true will result in blacking out tiles which do
not fall into the line of sight of the viewer.  Setting this to false
will not black out those tiles.


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

local tileEngineLayer = display.newGroup()

local tileEngine = TileEngine.Engine.new({
    parentGroup=tileEngineLayer,
    tileSize=32,
    spriteResolver=spriteResolver,
    compensateLightingForViewingPosition=true,
    hideOutOfSightElements=true
})
``````
