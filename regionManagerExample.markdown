# Example Using the RegionManager to Handle Very Large Worlds

The RegionManager provides a mechanism which enables the Wattage Tile
Engine to handle very large environments.  Environments which would
be too large to load into RAM.  It does this by only rendering smaller
"regions" as they become visible to the camera.  Your application
supplies these regions by implementing a listener which the RegionManager
can query for regions when they are needed.  Please refer to the
RegionManager [usage guide](regionManager/usageGuide.markdown) for more
details and definitions of terms used here.

# Setup

This example builds on the Wattage Tile Engine Template which
can be found [here](https://github.com/paulWatt526/wattageTileEngineAppTemplate).
The completed example can be found
[here](https://github.com/paulWatt526/wattageRegionManagerExample).

# Overview

In this example, the getRegion() listener function has been implemented
to supply horizontal hallways on even numbered region rows, vertical
hallways on even number region columns, and intersections where the
hallways intersect.  This results in a repeating pattern of crossing
hallways.  Physics bodies are also added and a collection of references
to them is attached to the region data returned by the listener function.
When the region needs to be overwritten with new data, the RegionManager
will call the regionReleased() listener function and pass the same region
data back to that function.  Having the physics bodies collection attached
to the region data enables the listener to cleanup the physics bodies
when they are no longer needed.  Please note that an actual implementation
of these listeners would likely be more complex resulting in a
non-patterned environment. This simple implementation is only meant
as an example.

This example also includes zooming functionality.  By zooming out very
far, one is able to see how the RegionManager repaints sub-regions
within the buffer layer as the player token moves.

# Code

A control stick class is used by this example.  It provides analog
directional movement.  Here is the code.

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local Utils = TileEngine.Utils

-- Localize external function calls.
local sqrt = math.sqrt
local min = math.min

local AnalogControlStick = {}
AnalogControlStick.new = function(params)
    Utils.requireParams({
        "parentGroup",
        "centerX",
        "centerY",
        "centerDotRadius",
        "outerCircleRadius"
    },params)

    local self = {}

    local touchId                                       -- Used to set touch focus on the control stick
    local centerDot                                     -- The center of the control stick
    local outerCircle                                   -- The outer circle of the control stick
    local outerCircleRadius = params.outerCircleRadius  -- private variable to store the outer circle radius

    -- Vector whose magnitude is a percentage of the radius from the center dot.  For example, if the outer
    -- ring of the control is touched, this vector would have a magnitude of 1, representing 100% of the radius.
    -- If the control was touched half way between the center dot and the outer ring, this vector would have a
    -- magnitude of 0.5 representing 50%.  If the touch point moves outside the radius, the value will be
    -- greater than 1 representing a value greater than 100%.  This can be used like a throttle control by
    -- setting an entity's velocity to a percentage of the max velocity.
    local currentRawDirectionVectorX
    local currentRawDirectionVectorY

    -- Same as currentRawDirectionVector except it is capped at 1 (or 100%).
    local currentDirectionVectorX
    local currentDirectionVectorY

    local function calculateDirectionVectors(x, y)
        -- Create vector for the control center point
        local centerPointVectorX = centerDot.x
        local centerPointVectorY = centerDot.y

        -- Create vector for the touch point
        local touchPointVectorX = x
        local touchPointVectorY = y

        -- Subtract the center vector from the touch point vector to get the control direction vector.
        local vectorToTouchPointX = touchPointVectorX - centerPointVectorX
        local vectorToTouchPointY = touchPointVectorY - centerPointVectorY

        -- Determine the magnitude of the vector
        local magnitude = sqrt(
            vectorToTouchPointX * vectorToTouchPointX + vectorToTouchPointY * vectorToTouchPointY)

        -- Determine the magnitude's percent of the outer circle radius
        local percent = magnitude / outerCircleRadius

        -- Store the capped percent.  This will result in any value greater than 1 being set to 1 instead.
        local cappedPercent = min(percent, 1)

        -- Calculates the vector where magnitude is the distance from the center dot represented as a
        -- percentage of the outer ring radius as described in the variable's declaration.
        currentRawDirectionVectorX = vectorToTouchPointX / magnitude * percent
        currentRawDirectionVectorY = vectorToTouchPointY / magnitude * percent

        -- Calculates the vector where magnitude is the distance from the center dot represented as a
        -- percentage of the outer ring radius and capped at 1 (100%) as described in the variable's declaration.
        currentDirectionVectorX = vectorToTouchPointX / magnitude * cappedPercent
        currentDirectionVectorY = vectorToTouchPointY / magnitude * cappedPercent
    end

    -- Handle for touch events
    local function touchHandler(event)
        -- If the control is already focused on a touch and this touch
        -- is not the current touch, exit early.
        if touchId ~= nil and touchId ~= event.id then
            return false
        end

        if event.phase == "began" then
            -- Touch has began

            -- Store the ID of the touch
            touchId = event.id

            -- Set the focus of the current touch to this control exclusively.
            display.getCurrentStage():setFocus(outerCircle, touchId)

            -- calculate the direction vectors
            calculateDirectionVectors(event.x, event.y)
        elseif event.phase == "moved" then
            -- Touch has moved

            -- calculate the direction vectors
            calculateDirectionVectors(event.x, event.y)
        elseif event.phase == "ended" or event.phase == "cancelled" then
            -- Touch has ended or was cancelled

            -- Remove the focus
            display.getCurrentStage():setFocus(outerCircle, nil)

            -- Clear the touchID
            touchId = nil

            -- Set direction vectors to nil
            currentRawDirectionVectorX = nil
            currentRawDirectionVectorY = nil
            currentDirectionVectorX = nil
            currentDirectionVectorY = nil
        end

        -- Indicate that the touch was handled by returning true
        return true
    end

    -- Return both the raw and capped vector values
    function self.getCurrentValues()
        return {
            cappedDirectionVector = {x = currentDirectionVectorX, y = currentDirectionVectorY},
            rawDirectionVector = {x = currentRawDirectionVectorX, y = currentRawDirectionVectorY}
        }
    end

    -- Perform cleanup of resources allocated by this class
    function self.destroy()
        outerCircle:removeEventListener("touch", touchHandler)
        display.getCurrentStage():setFocus(outerCircle, nil)
        outerCircle:removeSelf()
        outerCircle = nil

        centerDot:removeSelf()
        centerDot = nil
    end

    -- Initiallizes the managed resources
    local function initialize()
        centerDot = display.newCircle(
            params.parentGroup,
            params.centerX,
            params.centerY,
            params.centerDotRadius
        )
        centerDot:setFillColor(1,1,1,1)
        centerDot:setStrokeColor(1,1,1,1)
        centerDot.strokeWidth = 1
        centerDot.alpha = 0.25

        outerCircle = display.newCircle(
            params.parentGroup,
            params.centerX,
            params.centerY,
            params.outerCircleRadius
        )
        outerCircle:setFillColor(1,1,1,1)
        outerCircle.alpha = 0.25

        outerCircle:addEventListener("touch", touchHandler)
    end

    initialize()

    return self
end

return AnalogControlStick
``````


The example scene is listed here.  The comments within should be
adequate.  Please also reference the
[usage guide](regionManager/usageGuide.markdown) for more explanation.

``````lua
local AnalogControlStick = require "analogControlStick"
local Composer = require( "composer" )
local Physics = require "physics"
local TileEngine = require "plugin.wattageTileEngine"
local RegionManager = TileEngine.RegionManager

local scene = Composer.newScene()

-- Import file generated by PhysicsEditor which contains physics data for the tiles.
local scaleFactor = 1.0
local physicsData = (require "tilePhysicsBodies").physicsData(scaleFactor)

-- -----------------------------------------------------------------------------------
-- This table translates values used in the region templates to lookup names
-- used in the sprite sheet.
-- -----------------------------------------------------------------------------------
local REGION_VALUE_TO_TILE_NAME_MAP = {
    [0] = "tiles_00",
    [1] = "tiles_01",
    [2] = "tiles_02",
    [3] = "tiles_03",
    [4] = "tiles_04",
    [5] = "tiles_05",
    [6] = "tiles_06",
    [7] = "tiles_07",
    [8] = "tiles_08",
    [9] = "tiles_09",
    [10] = "tiles_10",
    [11] = "tiles_11",
    [12] = "tiles_12",
    [13] = "tiles_13",
    [14] = "tiles_14"
}

local VERTICAL_HALL_REGION = {
    {1,4,3},
    {1,4,3},
    {1,4,3}
}

local HORIZONTAL_HALL_REGION = {
    {2,2,2},
    {4,4,4},
    {0,0,0}
}

local CROSS_REGION = {
    { 5, 4, 12},
    { 4, 4,  4},
    {10, 4, 11}
}

local REGION_WIDTH_IN_TILES = 3             -- The width in tiles for each sub-region
local REGION_HEIGHT_IN_TILES = 3            -- The height in tiles for each sub-region
local BUFFER_TILE_LAYER_INDEX = 1           -- The layer index for the buffer tile layer
local ENTITY_LAYER_INDEX = 2                -- The layer index for the entity layer
local MIN_ZOOM = 0.1                        -- The minimum zoom level of the camera
local MAX_ZOOM = 2                          -- The maximum zoom level of the camera

local TILE_SIZE         = 128               -- Constant for the tile size
local BUFFER_LAYER_ROW_COUNT    = 180       -- Row count of the buffer layer
local BUFFER_LAYER_COLUMN_COUNT = 180       -- Column count of the buffer layer
local MAX_FORCE         = 500               -- The maximum force that will be applied to the player entity
local LINEAR_DAMPING    = 1                 -- Provides a little resistance to linear motion.

local tileEngine                            -- Reference to the tile engine
local lightingModel                         -- Reference to the lighting model
local tileEngineViewControl                 -- Reference to the UI view control
local regionManager                         -- Reference to the region manager
local controlStick                          -- Reference to the control stick
local playerEntityId                        -- ID used to interact with the player entity
local playerSprite                          -- Sprite for the player
local lastTime                              -- Used to track how much time passes between frames
local zoomInButton                          -- Reference to the zoom in button
local zoomOutButton                         -- Reference to the zoom out button
local curZoom                               -- The current camera zoom level
local isZoomingIn                           -- Flag set when zooming in
local isZoomingOut                          -- Flag set when zooming out
local touchId                               -- Used to track touches on zoom buttons

-- -----------------------------------------------------------------------------------
-- This will load in the example sprite sheet.
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
    -- Get the sprite sheet lookup name for the key value
    local name = REGION_VALUE_TO_TILE_NAME_MAP[key]

    -- Get the frame index for the lookup name
    local frameIndex = spriteSheetInfo:getFrameIndex(name)

    -- Retrieve the frame from the sprite sheet
    local frame = spriteSheetInfo.sheet.frames[frameIndex]

    -- Create the DisplayObject
    local displayObject = display.newImageRect(spriteSheet, frameIndex, frame.width, frame.height)

    -- Return a table containing the DisplayObject and its dimensions.
    return {
        imageRect = displayObject,
        width = frame.width,
        height = frame.height
    }
end

-- -----------------------------------------------------------------------------------
-- Handler for the zoom in button
-- -----------------------------------------------------------------------------------
local function zoomInHandler(event)
    -- If the control is already focused on a touch and this touch
    -- is not the current touch, exit early.
    if touchId ~= nil and touchId ~= event.id then
        return false
    end

    if event.phase == "began" then
        -- Touch has began

        -- Store the ID of the touch
        touchId = event.id

        -- Set the focus of the current touch to this control exclusively.
        display.getCurrentStage():setFocus(zoomInButton, touchId)

        -- Set zoom flag to true
        isZoomingIn = true
    elseif event.phase == "moved" then
        -- Touch has moved
    elseif event.phase == "ended" or event.phase == "cancelled" then
        -- Touch has ended or was cancelled

        -- Remove the focus
        display.getCurrentStage():setFocus(zoomInButton, nil)

        -- Clear the touchID
        touchId = nil

        -- Set zoom flag to false
        isZoomingIn = false
    end

    -- Indicate that the touch was handled by returning true
    return true
end

-- -----------------------------------------------------------------------------------
-- Handler for the zoom out button
-- -----------------------------------------------------------------------------------
local function zoomOutHandler(event)
    -- If the control is already focused on a touch and this touch
    -- is not the current touch, exit early.
    if touchId ~= nil and touchId ~= event.id then
        return false
    end

    if event.phase == "began" then
        -- Touch has began

        -- Store the ID of the touch
        touchId = event.id

        -- Set the focus of the current touch to this control exclusively.
        display.getCurrentStage():setFocus(zoomOutButton, touchId)

        -- Set zoom flag to true
        isZoomingOut = true
    elseif event.phase == "moved" then
        -- Touch has moved
    elseif event.phase == "ended" or event.phase == "cancelled" then
        -- Touch has ended or was cancelled

        -- Remove the focus
        display.getCurrentStage():setFocus(zoomOutButton, nil)

        -- Clear the touchID
        touchId = nil

        -- Set zoom flag to false
        isZoomingOut = false
    end

    -- Indicate that the touch was handled by returning true
    return true
end

-- -----------------------------------------------------------------------------------
-- This will be called every frame.  It is responsible for setting the camera
-- position, updating the lighting model, rendering the tiles, and reseting
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

        -- Get the direction vectors from the control stick
        local cappedPercentVector = controlStick.getCurrentValues().cappedDirectionVector

        -- If the control stick is currently being pressed, then apply the appropriate force
        if cappedPercentVector.x ~= nil and cappedPercentVector.y ~= nil then
            -- Determine the percent of max force to apply.  The magnitude of the vector from the
            -- conrol stick indicates the percentate of the max force to apply.
            local forceVectorX = cappedPercentVector.x * MAX_FORCE
            local forceVectorY = cappedPercentVector.y * MAX_FORCE
            -- Apply the force to the center of the player entity.
            playerSprite:applyForce(forceVectorX, forceVectorY, playerSprite.x, playerSprite.y)
        end

        -- Have the camera follow the player
        -- Use the RegionManager to get the location of the player entity
        -- Do NOT get the position directly from the x,y values on the sprite
        -- as they will not correctly reflect world coordinates.  Please reference
        -- the RegionManager usage guide for more info.
        local playerX, playerY = regionManager.getEntityLocation(2, playerEntityId)
        local tileXCoord = playerX / TILE_SIZE
        local tileYCoord = playerY / TILE_SIZE
        -- Set the camera location using the RegionManager.  Again, setting the
        -- location directly on the camera will not account for the world coordinate
        -- to local coordinate conversion.  Please reference
        -- the RegionManager usage guide for more info.
        regionManager.setCameraLocation(tileXCoord, tileYCoord)

        -- Determine curZoom
        if isZoomingIn then
            curZoom = curZoom * 1.05
            if curZoom > MAX_ZOOM then
                curZoom = MAX_ZOOM
            end
        end
        if isZoomingOut then
            curZoom = curZoom * 0.95
            if curZoom < MIN_ZOOM then
                curZoom = MIN_ZOOM
            end
        end

        -- It is ok to set the zoom level directly on the camera when using the RegionManager
        camera.setZoom(curZoom)

        -- Update the lighting model passing the amount of time that has passed since
        -- the last frame.
        lightingModel.update(deltaTime)
    else
        -- This is the first call to onFrame, so lastTime needs to be initialized.
        lastTime = event.time

        -- The initial camera zoom level is 1
        curZoom = 1

        -- This is the initial position of the camera set using the RegionManager.
        -- Its initial value is centered on the player entity location.
        regionManager.setCameraLocation(1.5,1.5)

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
-- This will create the physics objects for each region.
-- -----------------------------------------------------------------------------------
local function createPhysicsObjects(regionTemplate, topRowOffset, leftColumnOffset)
    local physicsObjects = {}

    -- Physics objects will be added to the tile engine's master
    -- group, but will not be visible.
    local physicsGroup = tileEngine.getMasterGroup()

    -- Iterate through the rows and columns of the region template.
    -- The template dimensions must match the dimensions specified
    -- to the RegionManager.
    for regionRow=1,REGION_HEIGHT_IN_TILES do
        for regionCol=1,REGION_WIDTH_IN_TILES do

            -- Obtain the value of the region tile
            local value = regionTemplate[regionRow][regionCol]

            -- Check to see if any physics bodies are associated with this tile value
            local firstPhysicsBody = physicsData:get(REGION_VALUE_TO_TILE_NAME_MAP[value])
            if firstPhysicsBody ~= nil then

                -- This tile value has physics bodies
                -- Calculate the center x, y coordinate where the physics
                -- body will be placed.  Use the offset values to properly
                -- place the body.  NOTE: regionCol and regionRow are reduced
                -- by 0.5 so that x and y reflect the center of the tile.
                local x = (leftColumnOffset + regionCol - 0.5) * TILE_SIZE
                local y = (topRowOffset + regionRow - 0.5) * TILE_SIZE

                -- Create an invisible displayObject to attach physics data to
                local physicsObject = display.newRect(
                    physicsGroup,
                    x,
                    y,
                    TILE_SIZE,
                    TILE_SIZE)
                physicsObject.isVisible = false

                -- Add the physics body information
                Physics.addBody(
                    physicsObject,
                    "static",
                    physicsData:get(REGION_VALUE_TO_TILE_NAME_MAP[value]))

                -- Add the physics objects to the collection
                table.insert(physicsObjects, physicsObject)
            end
        end
    end

    -- Return the collection of physics objects created here
    return physicsObjects
end

-- -----------------------------------------------------------------------------------
-- EndlessWorldRegionManager listener functions
--
-- This listener is responsible for supplying the region data to the RegionManager.
-- The absolute region row and column (which are the region coordinates relative to the world)
-- are passed to the function.  These coordinates should be used to determine what
-- data should be returned for the region.
--
-- The row and column offsets for the region are also passed to the function.  These
-- represent the offset in local coordinates in tile units to the top left corner of the region.
-- These coordinate offsets should be added to the local coordinates of any
-- additional objects added to this region (such as physics bodies).
--
-- This example function will place horizontal passages on even numbered rows,
-- vertical passages on even numbered columns, and crosses at the intersections.
-- However, this function could be much more complex to create more interesting
-- environments.
--
-- Physics objects created here are added to the returned table so they may be cleaned up
-- when the regionReleased() listener function is called.
-- -----------------------------------------------------------------------------------
function scene.getRegion(params)
    local absoluteRegionRow = params.absoluteRegionRow
    local absoluteRegionCol = params.absoluteRegionCol
    local topRowOffset = params.topRowOffset
    local leftColumnOffset = params.leftColumnOffset

    if absoluteRegionRow % 2 == 0 and absoluteRegionCol % 2 == 0 then
        local regionTemplate = CROSS_REGION
        local physicsObjects = createPhysicsObjects(regionTemplate, topRowOffset, leftColumnOffset)

        return {
            physicsObjects = physicsObjects,
            tilesByLayerIndex = {
                regionTemplate
            }
        }
    end

    if absoluteRegionRow % 2 == 0 then
        local regionTemplate = HORIZONTAL_HALL_REGION
        local physicsObjects = createPhysicsObjects(regionTemplate, topRowOffset, leftColumnOffset)

        return {
            physicsObjects = physicsObjects,
            tilesByLayerIndex = {
                regionTemplate
            }
        }
    end

    if absoluteRegionCol % 2 == 0 then
        local regionTemplate = VERTICAL_HALL_REGION
        local physicsObjects = createPhysicsObjects(regionTemplate, topRowOffset, leftColumnOffset)

        return {
            physicsObjects = physicsObjects,
            tilesByLayerIndex = {
                regionTemplate
            }
        }
    end

    return {}
end

-- -----------------------------------------------------------------------------------
-- This listener function is called when a region is no longer valid and
-- has been released.  Anything that was allocated and attached to the
-- regionData in the getRegion() function must be released here.  In this
-- example, the physics objects created in getRegion() need to be cleaned
-- up.
-- -----------------------------------------------------------------------------------
function scene.regionReleased(regionData)
    if regionData ~= nil and regionData.physicsObjects ~= nil then
        local physicsObjects = regionData.physicsObjects

        -- Release the physics objects, they are no longer valid.
        for i=1,#physicsObjects do
            physicsObjects[i]:removeSelf()
        end
        regionData.physicsObjects = nil
    end
end

-- -----------------------------------------------------------------------------------
-- Scene event functions
-- -----------------------------------------------------------------------------------

-- create()
function scene:create( event )
    local sceneGroup = self.view

    -- Start physics
    Physics.start()
    -- This example does not want any gravity, set it to 0.
    Physics.setGravity(0,0)
    -- Set scale (determined by trial and error for what feels right)
    Physics.setScale(32)

    -- Create a group to act as the parent group for all tile engine DisplayObjects.
    local tileEngineLayer = display.newGroup()
    sceneGroup:insert(tileEngineLayer)

    -- Create an instance of TileEngine.
    tileEngine = TileEngine.Engine.new({
        parentGroup=tileEngineLayer,
        tileSize=TILE_SIZE,
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
        isTransparent = function() return true end,             -- All tiles are transparent
        isTileAffectedByAmbient = function() return true end,   -- All tiles affected by ambient
        useTransitioners = false,
        compensateLightingForViewingPosition = false
    })

    -- Instantiate the module.
    local module = TileEngine.Module.new({
        name="moduleMain",
        rows= BUFFER_LAYER_ROW_COUNT,
        columns= BUFFER_LAYER_COLUMN_COUNT,
        lightingModel=lightingModel,
        losModel=TileEngine.LineOfSightModel.ALL_VISIBLE        -- All tiles are in line of sight
    })

    -- Next, create the buffer layer
    local bufferLayer = TileEngine.TileLayer.new({
        rows = BUFFER_LAYER_ROW_COUNT,
        columns = BUFFER_LAYER_COLUMN_COUNT
    })
    bufferLayer.setLightingMode(TileEngine.LayerConstants.LIGHTING_MODE_NONE)   -- Lighting data not used.
    bufferLayer.resetDirtyTileCollection()  -- No tiles are added directly to this layer, so go ahead and reset dirty tiles.

    -- Add the layer to the module at index 1 (indexes start at 1, not 0).  Set
    -- the scaling delta to zero (Scaling delta must be zero when using the RegionManager)
    module.insertLayerAtIndex(bufferLayer, BUFFER_TILE_LAYER_INDEX, 0)

    -- Next create the entity layer for the player token
    local entityLayer = TileEngine.EntityLayer.new({
        tileSize = TILE_SIZE,
        spriteResolver = spriteResolver
    })
    entityLayer.setLightingMode(TileEngine.LayerConstants.LIGHTING_MODE_NONE)   -- Lighting data not used.

    -- Add the entity layer to the module at index 2 (indexes start at 1, not 0).  Set
    -- the scaling delta to zero.
    module.insertLayerAtIndex(entityLayer, ENTITY_LAYER_INDEX, 0)

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

    -- Now create the endless world region manager.  Notice that
    -- no tiles have been added to the buffer layer.  This manager
    -- will utilize the listener passed in to query for regions of
    -- tiles when they are needed and will also inform the listener
    -- when regions have been released.
    regionManager = RegionManager.new({
        regionWidthInTiles = REGION_WIDTH_IN_TILES,
        regionHeightInTiles = REGION_HEIGHT_IN_TILES,
        renderRegionWidth = 5,                          -- 5 tiles wide is enough to fill an iPhone 6 screen
        renderRegionHeight = 3,                         -- 3 tiles high is enough to fill an iPhone 6 screen
        tileSize = 128,                                 -- Larger tiles will yeild higher performance as fewer of them are required to fill the screen
        tileLayersByIndex = { [BUFFER_TILE_LAYER_INDEX] = bufferLayer },    -- Table will all tile layers keyed by their index
        entityLayersByIndex = { [ENTITY_LAYER_INDEX] = entityLayer },       -- Table will all entity layers keyed by their index
        camera = tileEngineViewControl.getCamera(),     -- RegionManager will manage this camera by correctly transforming world and local coordinates.
        listener = scene                                -- The table containing the listener functions
    })

    -- Add the player entity to the entity layer
    local spriteInfo
    playerEntityId, spriteInfo = entityLayer.addEntity(14)

    -- Store a reference to the player entity sprite.  It will be
    -- used to apply forces to.
    playerSprite = spriteInfo.imageRect

    -- Make the player sprite a physical entity
    Physics.addBody( playerSprite, "dynamic", physicsData:get(REGION_VALUE_TO_TILE_NAME_MAP[14]) )

    -- Handle the player sprite as a bullet to prevent passing through walls
    -- when moving very quickly.
    playerSprite.isBullet = true

    -- This will prevent the player from "sliding" too much.
    playerSprite.linearDamping = LINEAR_DAMPING

    -- Move the player entity to the center of the middle cross.
    regionManager.centerEntityOnTile(2, playerEntityId, 1, 1)

    local radius = 150
    controlStick = AnalogControlStick.new({
        parentGroup = sceneGroup,
        centerX = display.screenOriginX + radius,
        centerY = display.screenOriginY + display.actualContentHeight - radius,
        centerDotRadius = 0.1 * radius,
        outerCircleRadius = radius
    })

    -- Create the zoom buttons
    zoomInButton = display.newImageRect(sceneGroup, "img/plus.png", 200, 200)
    zoomInButton.xScale = 0.5
    zoomInButton.yScale = 0.5
    zoomInButton.x = display.screenOriginX + display.actualContentWidth - 200
    zoomInButton.y = display.screenOriginY + display.actualContentHeight - 75

    zoomOutButton = display.newImageRect(sceneGroup, "img/minus.png", 200, 200)
    zoomOutButton.xScale = 0.5
    zoomOutButton.yScale = 0.5
    zoomOutButton.x = display.screenOriginX + display.actualContentWidth - 75
    zoomOutButton.y = display.screenOriginY + display.actualContentHeight - 75

    isZoomingIn = false
    isZoomingOut = false
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
        zoomInButton:addEventListener("touch", zoomInHandler)
        zoomOutButton:addEventListener("touch", zoomOutHandler)
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

        -- Remove zoom listeners
        zoomInButton:removeEventListener("touch", zoomInHandler)
        display.getCurrentStage():setFocus(zoomInButton, nil)
        isZoomingIn = false

        zoomOutButton:removeEventListener("touch", zoomOutHandler)
        display.getCurrentStage():setFocus(zoomOutButton, nil)
        isZoomingOut = false

        touchId = nil
    elseif ( phase == "did" ) then
        -- Code here runs immediately after the scene goes entirely off screen
    end
end


-- destroy()
function scene:destroy( event )

    local sceneGroup = self.view
    -- Code here runs prior to the removal of scene's view

    -- Release the zoom buttons
    zoomInButton:removeSelf()
    zoomInButton = nil
    zoomOutButton:removeSelf()
    zoomOutButton = nil

    -- Destroy regionManager (NOTE: This may result in calls to regionReleased() listener function)
    regionManager.destroy()
    regionManager = nil

    -- Destroy the tile engine instance to release all of the resources it is using
    tileEngine.destroy()
    tileEngine = nil

    -- Destroy the ViewControl to release all of the resources it is using
    tileEngineViewControl.destroy()
    tileEngineViewControl = nil

    -- Destroy the control stick
    controlStick.destroy()
    controlStick = nil

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

When run, the user is able to slide their finger along the control stick
and see the player token move in response.  The camera will follow the
player token.  The player token will not be able to move through walls.
The user may use the "+" and "-" buttons to zoom in and out.  By zooming
out very far, the user will be able to see how the RegionManager only
repaints smaller sub-regions of the buffer layer.  NOTE: Since this
example uses a repeating pattern, it may not look like previously
visited areas are being repainted when visited again.  However, they
are being repainted.

The code for this example can be found
[here](https://github.com/paulWatt526/wattageRegionManagerExample).

A video of the results can be found
[here](https://youtu.be/XOsp4bKpQ5Y).