# Example Loading a File from Tiled

Tiled is a popular tool for creating environments from tiles.  This
example will show how data can be extracted from a Tiled JSON file and
loaded into the engine.  This example will also illustrate the use of
the X and Y coefficients to achieve parallax scrolling.

# Setup

This example builds on the Wattage Tile Engine Template which
can be found [here](https://github.com/paulWatt526/wattageTileEngineAppTemplate).
The completed example, including a Tiled file and tileset can be found
[here](https://github.com/paulWatt526/wattagePlatformExample).
The version of Tiled used for this example is 0.15.1

# Walkthrough

Starting with the template, the following changes need to be made.

In the main file, set the background color to a pleasant sky blue
color.

``````lua
display.setDefault( "background", 0.4, 0.4, 1)
``````

In the config file, drop the resolution down to 320x480.

``````lua
application =
{
	content =
	{
		width = 320,
		height = 480,
		scale = "letterbox", -- zoom to fill screen, possibly cropping edges
		fps = 60
	},
}
``````

Inside the scene file, add an import for the Utils library.  Then
remove the default environment.  Next, add constants to store camera
speed and boundaries.

``````lua
local CAMERA_VELOCITY   = 5 / 1000          -- Camera velocity in tiles per second
local CAMERA_START_X    = 15                -- The start of the camera movement range
local CAMERA_END_X      = 60                -- The end of the camera movement range
``````

Add variables to store the number of rows and columns which will be
taken from the Tiled JSON file.

``````lua
local rowCount                              -- Row count of the environment
local columnCount                           -- Column count of the environment
``````

A small tweak is necessary for the SpriteResolver.  In this example,
there is no need to translate a string key into an index.  Instead
the index will be taken directly from the Tiled JSON file.

``````lua
local spriteResolver = {}
spriteResolver.resolveForKey = function(key)
    local frame = spriteSheetInfo.sheet.frames[key]
    local displayObject = display.newImageRect(spriteSheet, key, frame.width, frame.height)
    return TileEngine.SpriteInfo.new({
        imageRect = displayObject,
        width = frame.width,
        height = frame.height
    })
end
``````

Since lighting will only be from ambient, all tiles can be considered
transparent.  The isTransparent() callback is altered to reflect this.

``````lua
local function isTileTransparent(column, row)
    return true
end
``````

Add helper functions for loading a layer by name and for loading the
contents of those layers into the tile engine.

``````lua
-- -----------------------------------------------------------------------------------
-- This function is a convenience function to retrieve a layer from a Tiled file.
-- -----------------------------------------------------------------------------------
local function getLayerByName(name, levelDefinition)
    for i=1,#levelDefinition.layers do
        local curLayer = levelDefinition.layers[i]
        if curLayer.name == name then
            return curLayer
        end
    end
    return nil
end

-- -----------------------------------------------------------------------------------
-- This function is a convenience function to load tiles into a layer.
-- -----------------------------------------------------------------------------------
local function loadTilesIntoLayer(layer, layerData)
    for row=1, rowCount do
        for col=1, columnCount do
            local tileType = layerData.data[(row - 1) * columnCount + col]
            if tileType ~= 0 then
                layer.updateTile(
                    row,
                    col,
                    TileEngine.Tile.new({
                        resourceKey = tileType
                    }))
            end
        end
    end
end
``````

In the onFrame() function in the section that only runs on the first
frame, set the initial position of the camera.

``````lua
-- This is the initial position of the camera
camera.setLocation(CAMERA_START_X, 10)
``````

In the onFrame() function in the section that runs after the first
frame, update the position of the camera to bounce left and right.

``````lua
-- Update camera location
local newX = camera.getX() + deltaTime * CAMERA_VELOCITY
if newX > CAMERA_END_X then
    newX = newX - (newX - CAMERA_END_X)
    CAMERA_VELOCITY = -1 * CAMERA_VELOCITY
elseif newX < CAMERA_START_X then
    newX = newX + (CAMERA_START_X - newX)
    CAMERA_VELOCITY = -1 * CAMERA_VELOCITY
end
camera.setLocation(newX, camera.getY())
``````

Inside the scene:create() function are a number of changes.  First,
load in the JSON file and use the data to set the row and column
count.

``````lua
-- Load the Tiled JSON file
local levelDefinition = Utils.loadJsonFile("map.json")
rowCount = levelDefinition.height
columnCount = levelDefinition.width
``````

When instantiating the module, pass the row and column variables in.

``````lua
-- Instantiate the module.
local module = TileEngine.Module.new({
    name="moduleMain",
    rows= rowCount,
    columns= columnCount,
    lightingModel=lightingModel,
    losModel=TileEngine.LineOfSightModel.ALL_VISIBLE
})
``````

In the Tiled file, there are 5 layers: Clouds, Leaves, Trees, Platform1,
Platform2.  Each layer is loaded into the tile engine.

``````lua
-- Create a TileLayer for the clouds.
local cloudLayer = TileEngine.TileLayer.new({
    rows = rowCount,
    columns = columnCount
})
local cloudData = getLayerByName("Clouds", levelDefinition)
loadTilesIntoLayer(cloudLayer, cloudData)

-- Create a TileLayer for the leaves.
local leavesLayer = TileEngine.TileLayer.new({
    rows = rowCount,
    columns = columnCount
})
local leavesData = getLayerByName("Leaves", levelDefinition)
loadTilesIntoLayer(leavesLayer, leavesData)

-- Create a TileLayer for the trees.
local treeLayer = TileEngine.TileLayer.new({
    rows = rowCount,
    columns = columnCount
})
local treeData = getLayerByName("Trees", levelDefinition)
loadTilesIntoLayer(treeLayer, treeData)

-- Create a TileLayer for the platform 1.
local platform1Layer = TileEngine.TileLayer.new({
    rows = rowCount,
    columns = columnCount
})
local platform1Data = getLayerByName("Platform1", levelDefinition)
loadTilesIntoLayer(platform1Layer, platform1Data)

-- Create a TileLayer for the platform 2.
local platform2Layer = TileEngine.TileLayer.new({
    rows = rowCount,
    columns = columnCount
})
local platform2Data = getLayerByName("Platform2", levelDefinition)
loadTilesIntoLayer(platform2Layer, platform2Data)
``````

Now that the layers have been initialized, reset the dirty tiles
on all of them.

``````lua
-- It is necessary to reset dirty tile tracking after the layer has been
-- fully initialized.  Not doing so will result in unnecessary processing
-- when the scene is first rendered which may result in an unnecessary
-- delay (especially for larger scenes).
cloudLayer.resetDirtyTileCollection()
leavesLayer.resetDirtyTileCollection()
treeLayer.resetDirtyTileCollection()
platform1Layer.resetDirtyTileCollection()
platform2Layer.resetDirtyTileCollection()
``````

Insert the layers into the module.  In this case, no scaling delta
is needed between layers, so that will be set to 0.  An X coefficient
is needed to create the parallax scrolling.  The Platform2 layer should
follow the camera precisely, so its X coefficient is set to 1.  The
other layers need to move progressively slower than the camera so
they are set to values less than 1.

``````lua
-- Add the layers to the module starting at index 1 (indexes start at 1, not 0).
-- Set the scaling deltas to zero and stagger the X coefficients to create
-- parallax.
module.insertLayerAtIndex(cloudLayer, 1, 0, 0.6)
module.insertLayerAtIndex(leavesLayer, 2, 0, 0.7)
module.insertLayerAtIndex(treeLayer, 3, 0, 0.8)
module.insertLayerAtIndex(platform1Layer, 4, 0, 0.9)
module.insertLayerAtIndex(platform2Layer, 5, 0, 1)
``````

When run, the camera will automatically scroll right and left and
the layers will scroll at different rates.

The code for this stage can be found
[here](https://github.com/paulWatt526/wattagePlatformExample).

A video of the results can be found
[here](https://youtu.be/I_i6erwuDcI).