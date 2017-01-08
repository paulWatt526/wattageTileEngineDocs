# LineOfSightModel

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [LineOfSightModel](type_lineOfSightModel.markdown)
| __Library__          | [wattageTileEngine.*](../Readme.markdown)
| __Keywords__         | Wattage, LineOfSightModel, Tile Engine
| __See also__         |

## Overview

## Syntax

	local TileEngine = require "plugin.wattageTileEngine"

	-- Callback to indicate whether line of sight can pass through tile
    local function isTransparent(column, row)
        -- Make an opaque wall along column 5
        return column ~= 5
    end

	local lineOfSightModel = TileEngine.LineOfSightModel.new({
	    radius = 15,
	    isTransparent = isTransparent
	})

### Functions

##### [LineOfSightModel.new()](new.markdown)

##### [LineOfSightModel.update()](update.markdown)

##### [LineOfSightModel.makeDirty()](makeDirty.markdown)

##### [LineOfSightModel.hasDirtyTiles()](hasDirtyTiles.markdown)

##### [LineOfSightModel.resetDirtyFlags()](resetDirtyFlags.markdown)

##### [LineOfSightModel.isInLineOfSight()](isInLineOfSight.markdown)

##### [LineOfSightModel.getLineOfSightTransitionValue()](getLineOfSightTransitionValue.markdown)

##### [LineOfSightModel.resetChangeTracking()](resetChangeTracking.markdown)

##### [LineOfSightModel.getDirtyRows()](getDirtyRows.markdown)

##### [LineOfSightModel.getDirtyColumns()](getDirtyColumns.markdown)

##### [LineOfSightModel.getDirtyCount()](getDirtyCount.markdown)

##### [LineOfSightModel.getRowsTransitionedIn()](getRowsTransitionedIn.markdown)

##### [LineOfSightModel.getColsTransitionedIn()](getColsTransitionedIn.markdown)

##### [LineOfSightModel.getRowsTransitionedOut()](getRowsTransitionedOut.markdown)

##### [LineOfSightModel.getColsTransitionedOut()](getColsTransitionedOut.markdown)

##### [LineOfSightModel.getCoordinatesIn()](getCoordinatesIn.markdown)