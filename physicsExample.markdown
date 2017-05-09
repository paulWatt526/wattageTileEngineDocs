# Example Integrating Corona Physics Objects with the Wattage Tile Engine

The physics engine in Corona SDK supports three types of physics bodies:
Static, Dynamic, and Kinematic.  This example will show how to integrate
static and dynamic types.  It will not cover integrating kinematic types,
however, they would be handled in a way similar to how dynamic types
are handled.

Typically, using Corona SDK, one simply turns DisplayObjects into
physical entities directly.  So, one may expect to do the same within
the Wattage Tile Engine.  While this approach will work for DisplayObjects
in EntityLayers, it will not work for DisplayObjects in TileLayers.
This is because DisplayObjects are created and destroyed dynamically
by the tile engine in order to efficiently paint the tile layers.  So
the physical model associated with the TileLayers in your application
will need to be created as their own model.  This is not as cumbersome
as it may sound at first, as this example will illustrate.

_On a side note, this may lead one to ask why the tile engine doesn't
manage static physical objects in a similar way that it manages the
DisplayObjects for tiles.  In other words, why doesn't it dynamically
create and destroy them on demand depending on what is visible?  There
are a number of reasons for this:_

* _There has not yet been a need for us to do this.  While managing
tile DisplayObjects this way has resulted in dramatic performance
improvements, it has been our experience that the same cannot be said
about static physical objects._
* _This would prevent physics simulation from taking place outside
of the viewable area, which is likely not desirable in your application._
* _The physics model needed for the application may not directly match
the layout of the tiles._

# Setup

This example builds on the Wattage Tile Engine Template which
can be found [here](https://github.com/paulWatt526/wattageTileEngineAppTemplate).
The completed example can be found
[here](https://github.com/paulWatt526/wattagePhysicsExample).

# Overview

This example will start with the plus-sign-shaped room provided by the
template, then make the following changes:

* A physics model will be created to turn the walls into static physics
objects.
* An EntityLayer will be added and a player token will be added to this
layer.
* The sprite for the player token will be retrieved from the engine and
made into a physics object.
* An analog control stick will be added and its input will be used to
apply force to the player token in the direction specified by the
user's touch.  The force will be adjusted according to how far away from
the center of the control the touch falls.  This is meant to simulate an
analog control stick.
* The camera will be configured to follow the player token.

# Walkthrough

Starting with the template, the following changes need to be made.

The first change is to define the analog control stick.  A new file
was introduced called analogControlStick.lua which contains the new
code.  The code is copied below.  It is heavily commented, so further
explanation will not be given here.

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local Utils = TileEngine.Utils

-- Localize external function calls.
local sqrt = math.sqrt

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
        local magnitude = math.sqrt(
            vectorToTouchPointX * vectorToTouchPointX + vectorToTouchPointY * vectorToTouchPointY)

        -- Determine the magnitude's percent of the outer circle radius
        local percent = magnitude / outerCircleRadius

        -- Store the capped percent.  This will result in any value greater than 1 being set to 1 instead.
        local cappedPercent = math.min(percent, 1)

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

Require the new AnalogControlStick and the Physics library.

``````lua
local AnalogControlStick = require "analogControlStick"
local Physics = require "physics"
``````

In this example, the player token will have a maximum possible force to
apply when the analog control stick is at full throttle.  It will also
make use of linear damping to prevent the feeling of moving on ice.
These values are stored in the following constants.

``````lua
local TILE_SIZE         = 32                -- Constant for the tile size
local MAX_FORCE         = 10                -- The maximum force that will be applied to the player entity
local LINEAR_DAMPING    = 1                 -- Provides a little resistance to linear motion.
``````

When the physics objects are added, a filter needs to be specified to
indicate what objects can collide with others.  These categories are
defined below.

``````lua
local playerCategory = {categoryBits=1, maskBits=2} -- Category for the player physics object.  Will collide with walls.
local wallCategory = {categoryBits=2, maskBits=1}   -- Category for the wall physics objects.  Will collide with players.
``````

Add variables to store references to the control stick and to the player
sprite.

``````lua
local controlStick                          -- Reference to the control stick
local playerSprite                          -- Reference to the player sprite
``````

Create a helper function to create the physics model for the static
walls.

``````lua
-- -----------------------------------------------------------------------------------
-- A helper function to set up the physical environment.  This will add a static
-- box physics object for each wall tile.
-- -----------------------------------------------------------------------------------
local function addPhysicsObjectsForWalls(displayGroup, module)
    for row=1,ROW_COUNT do
        for col=1,COLUMN_COUNT do
            local value = ENVIRONMENT[row][col]
            if value == 1 then
                local displayObject = display.newRect(
                    displayGroup,
                    (col - 1) * TILE_SIZE + TILE_SIZE / 2,
                    (row - 1) * TILE_SIZE + TILE_SIZE / 2,
                    TILE_SIZE,
                    TILE_SIZE)
                displayObject.isVisible = false
                Physics.addBody(displayObject, "static", {
                    density=0.1,
                    friction=0.1,
                    filter=wallCategory
                })
                module.addPhysicsBody(displayObject)
            end
        end
    end
end
``````

In the section of onFrame() called after the first frame, gather the
input from the control stick and apply the appropriate force to the
player token.

``````lua
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
``````

In the same section of onFrame() update the camera to point at the player
token.

``````lua
-- Have the camera follow the player
local tileXCoord = playerSprite.x / TILE_SIZE
local tileYCoord = playerSprite.y / TILE_SIZE
camera.setLocation(tileXCoord, tileYCoord)
``````

In the scene:create() function, start up the physics engine.

``````lua
-- Start physics
Physics.start()
-- This example does not want any gravity, set it to 0.
Physics.setGravity(0,0)
-- Set scale (determined by trial and error for what feels right)
Physics.setScale(32)
``````

After setting up the floor TileLayer, create the physical model for the
walls by calling the helper function defined earlier.

``````lua
-- Add physics objects for the walls
addPhysicsObjectsForWalls(sceneGroup, module)
``````

Create the entity layer and add the player token to it.  Retrieve the
DisplayObject for the sprite (playerSprite) from the engine and make
it into a physics object.  Finally, insert the layer into the module
at index 2 above the floor layer.

``````lua
-- Add an entity layer for the player
local entityLayer = TileEngine.EntityLayer.new({
    tileSize = TILE_SIZE,
    spriteResolver = spriteResolver
})

-- Add the player entity to the entity layer
local entityId, spriteInfo = entityLayer.addEntity("tiles_2")

-- Move the player entity to the center of the environment.
entityLayer.centerEntityOnTile(entityId, 8, 8)

-- Store a reference to the player entity sprite.  It will be
-- used to apply forces to and to align the camera with.
playerSprite = spriteInfo.imageRect

-- Make the player sprite a physical entity
Physics.addBody(playerSprite, "dynamic", {
    density=1,
    friction=0.5,
    bounce=0.2,
    radius=12,
    filter= playerCategory
})

-- Handle the player sprite as a bullet to prevent passing through walls
-- when moving very quickly.
playerSprite.isBullet = true

-- This will prevent the player from "sliding" too much.
playerSprite.linearDamping = LINEAR_DAMPING

-- Add the entity layer to the module at index 2 (indexes start at 1, not 0).  Set
-- the scaling delta to zero.
module.insertLayerAtIndex(entityLayer, 2, 0)
``````

Instantiate the analog control stick.

``````lua
local radius = 150
controlStick = AnalogControlStick.new({
    parentGroup = sceneGroup,
    centerX = display.screenOriginX + radius,
    centerY = display.screenOriginY + display.viewableContentHeight - radius,
    centerDotRadius = 0.1 * radius,
    outerCircleRadius = radius
})
``````

In the scene:destroy() function, cleanup the control stick.

``````lua
controlStick.destroy()
controlStick = nil
``````

When run, the user is able to slide their finger along the control stick
and see the player token move in response.  The camera will follow the
player token.

The code for this example can be found
[here](https://github.com/paulWatt526/wattagePhysicsExample).

A video of the results can be found
[here](https://youtu.be/1yFL6uI-VGQ).