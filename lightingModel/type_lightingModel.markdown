# LightingModel

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [LightingModel](type_lightingModel.markdown)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Keywords__         | Wattage, LightingModel, Tile Engine
| __See also__         |

## Overview

The lighting model tracks lighting of the tiles.

## Syntax

``````lua
local TileEngine = require "plugin.wattageTileEngine"

-- Callback to indicate whether light can pass through a tile
local function isTransparentForLight(column, row)
    -- Make an opaque wall along column 5
    return column ~= 5
end

-- Callback to indicate whether a tile is affected by ambient lighting.
local function isTileAffectedByAmbient(row, column)
    -- Make all tiles affected by ambient lighting
    return true
end

local lightingModel = TileEngine.LightingModel.new({
    isTransparent = isTransparentForLight,
    isTileAffectedByAmbient = isTileAffectedByAmbient,
    useTransitioners = true
})
``````
### Constructor

##### [LightingModel.new()](new.markdown)


### Functions

##### [LightingModel.setAmbientLight()](setAmbientLight.markdown)

##### [LightingModel.getAmbientLight()](getAmbientLight.markdown)

##### [LightingModel.update()](update.markdown)

##### [LightingModel.resetDirtyFlags()](resetDirtyFlags.markdown)

##### [LightingModel.addLight()](addLight.markdown)

##### [LightingModel.updateLight()](updateLight.markdown)

##### [LightingModel.removeLight()](removeLight.markdown)

##### [LightingModel.getLightProperties()](getLightProperties.markdown)

##### [LightingModel.markLightAsDirtyIfAffectedAreaContainsTile()](markLightAsDirtyIfAffectedAreaContainsTile.markdown)

##### [LightingModel.getAggregateLightIfRowColumnOpaque()](getAggregateLightIfRowColumnOpaque.markdown)

##### [LightingModel.getAggregateLight()](getAggregateLight.markdown)

##### [LightingModel.getDirtyAggregateRows()](getDirtyAggregateRows.markdown)

##### [LightingModel.getDirtyAggregateColumns()](getDirtyAggregateColumns.markdown)

##### [LightingModel.getDirtyAggregateCount()](getDirtyAggregateCount.markdown)

##### [LightingModel.hasDirtyAggregateTile()](hasDirtyAggregateTile.markdown)

##### [LightingModel.hasAmbientLightChanged()](hasAmbientLightChanged.markdown)

##### [LightingModel.setIsTransparentCallback()](setIsTransparentCallback.markdown)

##### [LightingModel.setIsTileAffectedByAmbientCallback()](setIsTileAffectedByAmbientCallback.markdown)