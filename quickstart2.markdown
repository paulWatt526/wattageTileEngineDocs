# Quickstart

## Overview

This document is meant to get a developer up and running with the
Wattage Tile Engine as quickly as possible.  This document will
build upon the Wattage Tile Engine template which can be found
[here](https://github.com/paulWatt526/wattageTileEngineAppTemplate).

This document will first walk through the vanilla template, then
proceed to add features in the following stages:

* Stage 1 - Use the onFrame event handler to move the camera back and
forth.  This will illustrate how to move the camera.
* Stage 2 - Extrude the walls to illustrate how to use parallax.
* Stage 3 - Dim the ambient lighting and add two lights to show how
to use the lighting model.
* Stage 4 - Use the onFrame event handler to make the two lights
blink intermittently.  This will illustrate how to remove lights
from the lighting model.
* Stage 5 - Add a light which moves opposite the camera.  This will
illustrate how to update lights dynamically.
* Stage 6 - Add entities to move around.  This will illustrate how
to use the EntityLayer and show how lighting affects the shading
of the entities.
* Stage 7 - This stage will add a token to represent the player and
activate the line of sight feature of the engine.  This will
illustrate the engines capability of hiding areas that would not
be visible to the player.

Additional Examples

* Example Loading a Tiled File - This will illustrate how Tiled can be
used to create levels.

## Template Explanation

The template contains the boilerplate code needed to set up
a project for the Wattage Tile Engine.  It is hosted on Github
[here](https://github.com/paulWatt526/wattageTileEngineAppTemplate).
When run it should display a single plus sign shaped room as in the
following image:

![Screenshot of template running](img/templateScreenShot.png)

The template scene is copied below, and it contains comments
explaining the significance of each section.

``````lua
local Composer = require( "composer" )
local TileEngine = require "plugin.wattageTileEngine"

local scene = Composer.newScene()

-- -----------------------------------------------------------------------------------
-- This table represents a simple environment.  Replace this with
-- the model needed for your application.
-- -----------------------------------------------------------------------------------
local ENVIRONMENT = {
    {2,2,2,2,2,1,1,1,1,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {1,1,1,1,1,1,0,0,0,1,1,1,1,1,1},
    {1,0,0,0,0,0,0,0,0,0,0,0,0,0,1},
    {1,0,0,0,0,0,0,0,0,0,0,0,0,0,1},
    {1,0,0,0,0,0,0,0,0,0,0,0,0,0,1},
    {1,1,1,1,1,1,0,0,0,1,1,1,1,1,1},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,0,0,0,1,2,2,2,2,2},
    {2,2,2,2,2,1,1,1,1,1,2,2,2,2,2},
}

local ROW_COUNT         = #ENVIRONMENT      -- Row count of the environment
local COLUMN_COUNT      = #ENVIRONMENT[1]   -- Column count of the environment

local tileEngine                            -- Reference to the tile engine
local lightingModel                         -- Reference to the lighting model
local tileEngineViewControl                 -- Reference to the UI view control
local lastTime                              -- Used to track how much time passes between frames

-- -----------------------------------------------------------------------------------
-- This will load in the example sprite sheet.  Replace this with the sprite
-- sheet needed for your application.
-- -----------------------------------------------------------------------------------
local spriteSheetInfo = require "tiles"
local spriteSheet = graphics.newImageSheet("tiles.png", spriteSheetInfo:getSheet())

-- -----------------------------------------------------------------------------------
-- A sprite resolver is required by the engine.  Its function is to create a
-- SpriteInfo object for the supplied key.  This function will utilize the
-- example sprite sheet.
-- -----------------------------------------------------------------------------------
local spriteResolver = {}
spriteResolver.resolveForKey = function(key)
    local frameIndex = spriteSheetInfo:getFrameIndex(key)
    local frame = spriteSheetInfo.sheet.frames[frameIndex]
    local displayObject = display.newImageRect(spriteSheet, frameIndex, frame.width, frame.height)
    return TileEngine.SpriteInfo.new({
        imageRect = displayObject,
        width = frame.width,
        height = frame.height
    })
end

-- -----------------------------------------------------------------------------------
-- A simple helper function to add floor tiles to a layer.
-- -----------------------------------------------------------------------------------
local function addFloorToLayer(layer)
    for row=1,ROW_COUNT do
        for col=1,COLUMN_COUNT do
            local value = ENVIRONMENT[row][col]
            if value == 0 then
                layer.updateTile(
                    row,
                    col,
                    TileEngine.Tile.new({
                        resourceKey="tiles_0"
                    })
                )
            elseif value == 1 then
                layer.updateTile(
                    row,
                    col,
                    TileEngine.Tile.new({
                        resourceKey="tiles_1"
                    })
                )
            end
        end
    end
end

-- -----------------------------------------------------------------------------------
-- This is a callback required by the lighting model to determine whether a tile
-- is transparent.  In this implementation, the cells with a value of zero are
-- transparent.  The engine may ask about the transparency of tiles that are outside
-- the boundaries of our environment, so the implementation must handle these cases.
-- That is why nil is checked for in this example callback.
-- -----------------------------------------------------------------------------------
local function isTileTransparent(column, row)
    local rowTable = ENVIRONMENT[row]
    if rowTable == nil then
        return true
    end
    local value = rowTable[column]
    return value == nil or value == 0
end

-- -----------------------------------------------------------------------------------
-- This is a callback required by the lighting model to determine whether a tile
-- should be affected by ambient light.  This simple implementation always returns
-- true which indicates that all tiles are affected by ambient lighting.  If an
-- environment had a section which should not be affected by ambient lighting, this
-- callback can be used to indicate that.  For example, the environment my be
-- an outdoor environment where the ambient lighting is the sun.  A few tiles in this
-- environment may represent the inside of a cabin, and these tiles would need to
-- not be affected by ambient lighting.
-- -----------------------------------------------------------------------------------
local function allTilesAffectedByAmbient(column, row)
    return true
end

-- -----------------------------------------------------------------------------------
-- This will be called every frame.  It is responsible for setting the camera
-- positiong, updating the lighting model, rendering the tiles, and reseting
-- the dirty tiles on the lighting model.
-- -----------------------------------------------------------------------------------
local function onFrame(event)
    local camera = tileEngineViewControl.getCamera()
    local lightingModel = tileEngine.getActiveModule().lightingModel

    if lastTime ~= 0 then
        -- Determine the amount of time that has passed since the last frame and
        -- record the current time in the lastTime variable to be used in the next
        -- frame.
        local curTime = event.time
        local deltaTime = curTime - lastTime
        lastTime = curTime

        -- Update the lighting model passing the amount of time that has passed since
        -- the last frame.
        lightingModel.update(deltaTime)
    else
        -- This is the first call to onFrame, so lastTime needs to be initialized.
        lastTime = event.time

        -- This is the initial position of the camera
        camera.setLocation(7.5, 7.5)

        -- Since a time delta cannot be calculated on the first frame, 1 is passed
        -- in here as a placeholder.
        lightingModel.update(1)
    end

    -- Render the tiles visible to the passed in camera.
    tileEngine.render(camera)

    -- The lighting model tracks changes, then acts on all accumulated changes in
    -- the lightingModel.update() function.  This call resets the change tracking
    -- and must be called after lightingModel.update().
    lightingModel.resetDirtyFlags()
end

-- -----------------------------------------------------------------------------------
-- Scene event functions
-- -----------------------------------------------------------------------------------

-- create()
function scene:create( event )
    local sceneGroup = self.view

    -- Create a group to act as the parent group for all tile engine DisplayObjects.
    local tileEngineLayer = display.newGroup()

    -- Create an instance of TileEngine.
    tileEngine = TileEngine.Engine.new({
        parentGroup=tileEngineLayer,
        tileSize=32,
        spriteResolver=spriteResolver,
        compensateLightingForViewingPosition=false,
        hideOutOfSightElements=false
    })

    -- The tile engine needs at least one Module.  It can support more than
    -- one, but this template sets up only one which should meet most use cases.
    -- A module is composed of a LightingModel and a number of Layers
    -- (TileLayer or EntityLayer).  An instance of the lighting model is created
    -- first since it is needed to instantiate the Module.
    lightingModel = TileEngine.LightingModel.new({
        isTransparent = isTileTransparent,
        isTileAffectedByAmbient = allTilesAffectedByAmbient,
        useTransitioners = false,
        compensateLightingForViewingPosition = false
    })

    -- Instantiate the module.
    local module = TileEngine.Module.new({
        name="moduleMain",
        rows=ROW_COUNT,
        columns=COLUMN_COUNT,
        lightingModel=lightingModel,
        losModel=TileEngine.LineOfSightModel.ALL_VISIBLE
    })

    -- Next, layers will be added to the Module...

    -- Create a TileLayer for the floor.
    local floorLayer = TileEngine.TileLayer.new({
        rows = ROW_COUNT,
        columns = COLUMN_COUNT
    })

    -- Use the helper function to populate the layer.
    addFloorToLayer(floorLayer)

    -- It is necessary to reset dirty tile tracking after the layer has been
    -- fully initialized.  Not doing so will result in unnecessary processing
    -- when the scene is first rendered which may result in an unnecessary
    -- delay (especially for larger scenes).
    floorLayer.resetDirtyTileCollection()

    -- Add the layer to the module at index 1 (indexes start at 1, not 0).  Set
    -- the scaling delta to zero.
    module.insertLayerAtIndex(floorLayer, 1, 0)

    -- Add the module to the engine.
    tileEngine.addModule({module = module})

    -- Set the module as the active module.
    tileEngine.setActiveModule({
        moduleName = "moduleMain"
    })

    -- To render the tiles to the screen, create a ViewControl.  This example
    -- creates a ViewControl to fill the entire screen, but one may be created
    -- to fill only a portion of the screen if needed.
    tileEngineViewControl = TileEngine.ViewControl.new({
        parentGroup = sceneGroup,
        centerX = display.contentCenterX,
        centerY = display.contentCenterY,
        pixelWidth = display.actualContentWidth,
        pixelHeight = display.actualContentHeight,
        tileEngineInstance = tileEngine
    })

    -- Finally, set the ambient light to white light with medium-high intensity.
    lightingModel.setAmbientLight(1,1,1,0.7)
end


-- show()
function scene:show( event )
    local sceneGroup = self.view
    local phase = event.phase

    if ( phase == "will" ) then
        -- Code here runs when the scene is still off screen (but is about to come on screen)

        -- Set the lastTime variable to 0.  This will indicate to the onFrame event handler
        -- that it is the first frame.
        lastTime = 0

        -- Register the onFrame event handler to be called before each frame.
        Runtime:addEventListener( "enterFrame", onFrame )
    elseif ( phase == "did" ) then
        -- Code here runs when the scene is entirely on screen
    end
end


-- hide()
function scene:hide( event )
    local sceneGroup = self.view
    local phase = event.phase

    if ( phase == "will" ) then
        -- Code here runs when the scene is on screen (but is about to go off screen)

        -- Remove the onFrame event handler.
        Runtime:removeEventListener( "enterFrame", onFrame )
    elseif ( phase == "did" ) then
        -- Code here runs immediately after the scene goes entirely off screen
    end
end


-- destroy()
function scene:destroy( event )

    local sceneGroup = self.view
    -- Code here runs prior to the removal of scene's view

    -- Destroy the tile engine instance to release all of the resources it is using
    tileEngine.destroy()
    tileEngine = nil

    -- Destroy the ViewControl to release all of the resources it is using
    tileEngineViewControl.destroy()
    tileEngineViewControl = nil

    -- Set the reference to the lighting model to nil.
    lightingModel = nil
end


-- -----------------------------------------------------------------------------------
-- Scene event function listeners
-- -----------------------------------------------------------------------------------
scene:addEventListener( "create", scene )
scene:addEventListener( "show", scene )
scene:addEventListener( "hide", scene )
scene:addEventListener( "destroy", scene )
-- -----------------------------------------------------------------------------------

return scene
``````

## Quickstart Stages

If you haven't done so already, pull down the template project from
Github [here](https://github.com/paulWatt526/wattageTileEngineAppTemplate)
and follow through the changes introduced in each of the following stages.

### Quickstart Stage 1

This stage will use the onFrame event handler to move the camera left
and right.  The first change necessary is inside of the onFrame function.
The initial position of the camera has been changed to the first tile
on the left of the room.

``````lua
-- This is the initial position of the camera
camera.setLocation(0.5, 7.5)
``````

The motion of the camera will move right then left and repeat.  To
implement this, the X position will increase until greater than or equal
to 14.5, then decrease until less than or equal to 0.5 and repeat.

Two variables will be introduced, one to specify the speed and one to
indicate the current direction.

``````lua
local CAMERA_SPEED      = 4 / 1000          -- Camera speed, 4 tiles per second
local cameraDirection                       -- Tracks the direction of the camera
``````

Initialize cameraDirection inside the scene:show() function.

``````lua
cameraDirection = "right"
``````

Finally, add the movement logic in the onFrame function.

``````lua
-- Update the position of the camera
local curXPos = camera.getX()
local xDelta = CAMERA_SPEED * deltaTime
if cameraDirection == "right" then
    curXPos = curXPos + xDelta
    if curXPos > 14.5 then
        cameraDirection = "left"
        curXPos = 14.5 - (curXPos - 14.5)
    end
else
    curXPos = curXPos - xDelta
    if curXPos < 0.5 then
        cameraDirection = "right"
        curXPos = 0.5 + (0.5 - curXPos)
    end
end
camera.setLocation(curXPos, camera.getY())
``````

The code for this stage can be found
[here](https://github.com/paulWatt526/tileEngineQuickStart1).

A video of the results can be found
[here](https://youtu.be/nhX8XCfxSEM).

### Quickstart Stage 2

At this point, a camera is moving left and right above a plus sign
shaped room.  Its nice, but it looks a little flat.  In this stage
the walls will be extruded to give a sense of depth.

Add two constants to allow for tweaking.  One will indicate how many
extruded layers to create and the other will indicate the scaling
delta between layers.

``````lua
local WALL_LAYER_COUNT  = 4                 -- The number of extruded wall layers
local SCALING_DELTA     = 0.04              -- The scaling delta between wall layers
``````

Next add a helper function to add the wall tiles to the new layers.

``````lua
-- -----------------------------------------------------------------------------------
-- A simple helper function to add walls to a layer.
-- -----------------------------------------------------------------------------------
local function addWallsToLayer(layer)
    for row=1,ROW_COUNT do
        for col=1,COLUMN_COUNT do
            local value = ENVIRONMENT[row][col]
            if value == 1 then
                layer.updateTile(
                    row,
                    col,
                    TileEngine.Tile.new({
                        resourceKey="tiles_1"
                    }))
            end
        end
    end
end
``````

Inside the scene:create() function, add the additional layers.  It is
important to reset the dirty tiles after creating each layer.  Not doing
so will result in unnecessary processing on the first render.  Each
layer will be added at the next index value.  This results in adding
each layer on top of the previous one.  A scaling delta is also applied
to each layer.  This indicates the difference in scaling from the previous
layer.  This scaling delta is what results in the parallax scrolling.

``````lua
-- Create extruded wall layers
for i=1,WALL_LAYER_COUNT do
    local wallLayer = TileEngine.TileLayer.new({
        rows = ROW_COUNT,
        columns = COLUMN_COUNT
    })
    addWallsToLayer(wallLayer)
    wallLayer.resetDirtyTileCollection()
    module.insertLayerAtIndex(wallLayer, i + 1, SCALING_DELTA)
end
``````

The code for this stage can be found
[here](https://github.com/paulWatt526/tileEngineQuickStart2).

A video of the results can be found
[here](https://youtu.be/6HMTZswe3Rc).

### Quickstart Stage 3

At this point, there is a moving camera and extruded walls.  Next, a
light will be added to the scene.

First add a variable to store the light ID.

``````lua
local topLightId                            -- Will track the ID of the top light
``````

Within the scene:create() function, add a slightly yellowish light at
the top, and dim the ambient lighting considerably.

``````lua
-- Add a light at the top part of the room.
topLightId = lightingModel.addLight({
    row=5,column=8,r=1,g=1,b=0.7,intensity=0.75,radius=9
})

-- Finally, set the ambient light to white light with medium-high intensity.
lightingModel.setAmbientLight(1,1,1,0.15)
``````

This will result in a much more dramatically lit environment.  Feel free
to tweak the light position, color, intensity, and radius to see how
they modify the results.

The code for this stage can be found
[here](https://github.com/paulWatt526/tileEngineQuickStart3).

A video of the results can be found
[here](https://youtu.be/eaU-ujjuLNA).

### Quickstart Stage 4

### Quickstart Stage 5

### Quickstart Stage 6

### Quickstart Stage 7