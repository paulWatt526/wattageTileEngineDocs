# EntityLayer

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [EntityLayer](type_entityLayer.markdown)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Keywords__         | Wattage, EntityLayer, Layer, Tile Engine
| __See also__         |

## Overview

The entity layer enables arbitrary placement of entities resolved by
the supplied sprite resolver or any display object.

## Syntax

``````lua
local TileEngine = require "plugin.wattageTileEngine"

local entityLayer = TileEngine.EntityLayer.new({
    tileSize=32,
    spriteResolver=spriteResolver
})
``````

### Constructor

##### [EntityLayer.new()](new.markdown)

### Functions

##### [EntityLayer.clear()](clear.markdown)

##### [EntityLayer.addEntity()](addEntity.markdown)

##### [EntityLayer.addNonResourceEntity()](addNonResourceEntity.markdown)

##### [EntityLayer.removeEntity()](removeEntity.markdown)

##### [EntityLayer.removeNonResourceEntity()](removeNonResourceEntity.markdown)

##### [EntityLayer.centerEntityOnTile()](centerEntityOnTile.markdown)

##### [EntityLayer.centerNonResourceEntityOnTile()](centerNonResourceEntityOnTile.markdown)

##### [EntityLayer.setEntityTilePosition()](setEntityTilePosition.markdown)

##### [EntityLayer.getEntityTilePosition()](getEntityTilePosition.markdown)

##### [EntityLayer.setNonResourceEntityTilePosition()](setNonResourceEntityTilePosition.markdown)

##### [EntityLayer.getNonResourceEntityTilePosition()](getNonResourceEntityTilePosition.markdown)

##### [EntityLayer.getEntityInfo()](getEntityInfo.markdown)

##### [EntityLayer.getEntityInfos()](getEntityInfos.markdown)

##### [EntityLayer.destroy()](destroy.markdown)