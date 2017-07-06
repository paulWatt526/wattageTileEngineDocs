# RegionManager Usage Guide

The RegionManager provides a way to load and unload smaller regions of a
world as they move into and out of the camera's view.  This enables the
Wattage Tile Engine to work with very large worlds which would not fit
into memory if loaded in their entirety.

## Using the Wattage Tile Engine without the RegionManager

Many applications do not require very large worlds.  In these cases,
applications are able to load complete environments into memory without
issue.  In this use case, the developer would typically perform the
following tasks:

1. Create a TileLayer in the engine large enough to hold the environment.
2. Load the environment into the TileLayer.
3. Move the camera around the TileLayer to render views to the user.
4. Set the positions of entities within the environment to display
them at those locations.

This approach works for the majority of cases.  However, what if your
app needs to display a very large world which is too big to fit into
RAM?  Or how about the case where the world is procedurally generated
and absolutely huge?  Enter the RegionManager.

## Using the Wattage Tile Engine with the RegionManager

The RegionManager does not load the entire environment into the
TileLayer at once.  It instead uses the TileLayer as a buffer.  The
TileLayer is divided into sub-regions of a defined size and the
RegionManager loads data into the sub-regions and releases data from
them as they move into and out of the camera's view.  The developer is
responsible for implementing a listener to receive the load and unload
events and handle them properly.  The developer should not call the
TileLayer.updateTile() function directly when using the RegionManager.

There is an issue with using the TileLayer as a buffer in this way, and
that issue is the issue of coordinate spaces.  To interact with this
layer as though it were very large (much bigger that it actually is),
it becomes necessary to adjust camera and entity world positions into
layer local positions.  This can get very confusing and is not something
the developer should have to concern themselves with.  For this reason,
the RegionManager has been created to handle all of this behind the
scenes.  This requires the developer to interact with the camera and
entities through the interface exposed by the RegionManager instead of
directly with the camera and entities.

Before going further, let's review some terminology.  Refer to the
diagram below:

![Region diagram](../img/RegionManagerDiagram.png)

* ***World Coordinates*** - This refers to world coordinates which can
be very large.
* ***Local Coordinates*** - This refers to coordinates local to the
layer.  World coordinates need to be converted to layer coordinates and
layer coordinates need to be converted back into world coordinates.
* ***Tile Layer*** - This is represented by the entire image.
* ***Sub Region*** - A partition of the Tile Layer which is a configurable
number of tiles wide and high.  The sub regions are indicated by the
green grid in the image.  These are the areas that the listener function
will need to supply and cleanup.
* ***Render Regions*** - This is an area defined by a number of regions
high and wide.  The center sub-region of this area will follow the
camera and always contain the camera.  The render region is highlighted
in blue.  These tiles will be kept up-to-date by the RegionManager and
represent the maximum number of regions that can be requested from the
listener in a single frame.  Usually, the number of regions requested
will be less than half of this total.
* ***Active Region*** - The Render Regions (highlighted in blue) can never span an
edge of a layer.  So as the center region of the render regions follows
the camera, it can never be positioned outside of the red area.  The
red area is called the "Active Region".  When it becomes necessary
for the the center region of the render region to leave the red area,
the blue region is moved to the opposite side of the layer, the
coordinate conversions are updated to continue to correctly convert
world coordinates into layer coordinates, and the entity positions
are updated to offset them appropriately.  Leaving the red area is
an example of a time when all blue regions will be requested from the
listener.

The dimensions of all of these regions are configured when creating
the RegionManager and must meet the following validations:

* All layers managed by the RegionManager must have the same dimensions.
* The layer width and height must be even numbers.
* The layer tile width must be evenly divisible by the sub-region tile width.
* The layer tile height must be evenly divisible by the sub-region tile height.
* The number of sub-regions in a horizontally across a layer must be an even number.
* The number of sub-regions in a vertically across a layer must be an even number.
* Render Regions width must be an odd number.
* Render Regions height must be an odd number.
* The layer must have at least 3 times the number of horizontal
sub-regions as the number of render regions in a row.
* The layer must have at least 3 times the number of vertical
sub-regions as the number of render regions in a col.

Tasks performed by the developer when using the RegionManager are the
following:

1. Determine the width and height of the regions in tile units.
2. Create a TileLayer such that it meets the validations listed above.
3. Create the RegionManager and register the following with it:
    * A listener to handle supplying region data and cleaning it up.
    * TileLayers - RegionManager will handle updating the tiles
    * EntityLayers - RegionManager will adjust the position of entities
    in these layers as the local coordinate conversions are adjusted.
4. Move the camera and entities using the functions provided by the
RegionManager.  The developer should **NOT** interact with the camera
or entities directly.

### Implementing the Listener

The RegionManager requires the developer to supply a listener which
has references to two functions:

``````lua
getRegion(params)

regionReleased(regionData)
``````

#### Implementing getRegion()

getRegion(params) is supplied with a table containing the following:
* ***absoluteRegionRow*** - The 0-based row number of the region being
requested.  Note, this can be negative.
* ***absoluteRegionCol*** - The 0-based column number of the region being
requested.  Note, this can be negative.
* ***topRowOffset*** - The row offset for the upper edge of the region.
Useful when adding entities or physics bodies with the region.
* ***leftColumnOffset*** - The column offset for the left edge of the region.
Useful when adding entities or physics bodies with the region.

The implementation of getRegion() may return an empty table in the case
of an empty region.  However, if the region is to contain tiles, the
returned table must contain a nested table called tilesByLayerIndex
which contains 2-dimensional 1-based arrays of tile values indexed by
the index of the layer they are to be inserted into.  The values in
these 2-dimensional arrays must be resolvable by the SpriteResolver
supplied to the engine.

The developer may also attach anything else to the table that may be
useful for cleanup.  This same table will be passed to the
regionReleased() function when the region is no longer needed.  This
is a handy way to track and release static physics objects in the region.

The following example implements the getRegion() listener function to
return a region with a block in the center of it for every other row and column.
It also attaches the physics object created for it so it can be released later.
``````lua
local TILE_SIZE = 128
local DOT_REGION = {
    { 0, 0, 0},
    { 0, 1, 0},
    { 0, 0, 0}
}

local listener = {}
function listener.getRegion(params)
    local absoluteRegionRow = params.absoluteRegionRow
    local absoluteRegionCol = params.absoluteRegionCol
    local topRowOffset = params.topRowOffset
    local leftColumnOffset = params.leftColumnOffset

    if absoluteRegionRow % 2 == 0 and absoluteRegionCol % 2 == 0 then
        local regionTemplate = DOT_REGION
        local x = (leftColumnOffset + 2 - 0.5) * TILE_SIZE
        local y = (topRowOffset + 2 - 0.5) * TILE_SIZE
        local physicsObject = display.newRect(x, y, TILE_SIZE, TILE_SIZE)
        Physics.addBody(displayObject, "static", {
            density=0.1,
            friction=0.1,
            filter=1
        })
        return {
            physicsObjects = {physicsObject},
            tilesByLayerIndex = {
                regionTemplate
            }
        }
    end

    return {}
end
``````

#### Implementing regionReleased()

regionReleased(regionData) is supplied with the same regionData table
which was provided by getRegion().  The implementation should clean up
anything that getRegion() allocated and attached to the regionData table.
This is a handy way to track and release static physics objects in the
region.  If nothing additional was allocated in the getRegion() function,
then this function need not do anything.

This example releases the physicsObjects attached to the regionData.

``````lua
function listener.regionReleased(regionData)
    if regionData ~= nil and regionData.physicsObjects ~= nil then
        local physicsObjects = regionData.physicsObjects

        -- Release the physics objects, they are no longer valid.
        for i=1,#physicsObjects do
            physicsObjects[i]:removeSelf()
        end
        regionData.physicsObjects = nil
    end
end
``````

### Instantiating the RegionManager

``````lua
local camera
local bufferLayer
local entityLayer
local listener = {}
listener.getRegion = function(params)
end
listener.regionReleased = function(regionData)
end

local regionManager = RegionManager.new({
    regionWidthInTiles = 3,
    regionHeightInTiles = 3,
    renderRegionWidth = 5,
    renderRegionHeight = 3,
    tileSize = 128,
    tileLayersByIndex = { [1] = bufferLayer },
    entityLayersByIndex = { [2] = entityLayer },
    camera = camera,
    listener = listener
})
``````

### Using the RegionManager

Using the RegionManager, it is possible to position the camera and entities
using world coordinates.  The RegionManager will handle all of the conversions
for you.

Get entity positions like the following:

``````lua
local entityLayerIndex = 2
local entityId = 42
local entityX, entityY = regionManager.getEntityLocation(entityLayerIndex, entityId)
``````

...or for non-resource entities, do the following:

``````lua
local entityLayerIndex = 2
local nonResourceEntityId = 42
local entityX, entityY = regionManager.getNonResourceEntityLocation(entityLayerIndex, nonResourceEntityId)
``````

Update the camera like the following:

``````lua
local tileXCoord = entityX / TILE_SIZE
local tileYCoord = entityY / TILE_SIZE
regionManager.setCameraLocation(tileXCoord, tileYCoord)
``````

Update entity positions like the following:

``````lua
local entityLayerIndex = 2
local entityId = 42
regionManager.centerEntityOnTile(entityLayerIndex, entityId, 1, 1)

-- OR

regionManager.setEntityLocation(entityLayerIndex, entityId, 192, 192)
``````

...or for non-resource entities, do the following:

``````lua
local entityLayerIndex = 2
local nonResourceEntityId = 42
regionManager.centerNonResourceEntityOnTile(entityLayerIndex, nonResourceEntityId, 1, 1)

-- OR

regionManager.setNonResourceEntityLocation(entityLayerIndex, nonResourceEntityId, 192, 192)
``````

### Performance Considerations

* Consider using larger tile sizes.  Larger tile sizes result in fewer
tiles being on the screen at once.
* Keep the region sizes as small as possible.  Keeping them small
reduces the number of updates performed in a frame.
* Do not define a render region larger than is necessary to fill the
view.
* Create as large a buffer layer as reasonably possible.  The biggest
performance hit occurs when the camera crosses the edge of the
active region.  Having a larger buffer will reduce the frequency of these
occurrences.

### Gotchas

* Parallax Scrolling using layer scaling or scrolling coefficients
is not possible when using the RegionManager.

### Example

[RegionManager Example Project](../regionManagerExample.markdown)