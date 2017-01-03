# Engine

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Engine](type_engine.markdown)
| __Corona Store__     | [wattageTileEngine](http://store.coronalabs.com/plugin/wattageTileEngine)
| __Keywords__         | Wattage, Engine, Tile Engine
| __See also__         |

## Overview

The engine handles the rendering of all of the layers.

## Syntax

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

### Functions


##### [Engine.addModule()](addModule.markdown)

##### [Engine.getActiveModule()](getActiveModule.markdown)

##### [Engine.getMasterGroup()](getMasterGroup.markdown)

##### [Engine.getTileSize()](getTileSize.markdown)

##### [Engine.isTileVisibleInLayer()](isTileVisibleInLayer.markdown)

##### [Engine.new()](new.markdown)

##### [Engine.removeModule()](removeModule.markdown)

##### [Engine.render()](render.markdown)

##### [Engine.setActiveModule()](setActiveModule.markdown)

##### [Engine.update()](update.markdown)