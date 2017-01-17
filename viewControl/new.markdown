# ViewControl.new()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ViewControl.*](type_viewControl.markdown)
| __Return value__     | [ViewControl](type_viewControl.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function creates a new instance of ViewControl.


## Syntax

	ViewControl.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### parentGroup <small>(required)</small>
_[DisplayObject](https://docs.coronalabs.com/api/type/DisplayObject/index.html)._
The parent DisplayGroup for the view control.

##### centerX <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The X position for the center of the view control.

##### centerY <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The Y position for the center of the view control.

##### pixelWidth <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The width of the control in pixels.

##### pixelHeight <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The height of the control in pixels.

##### tileEngineInstance <small>(required)</small>
_[TileEngine](../engine/type_engine.markdown)._
The instance of the tile engine that this view control will be
displaying.

##### useContainer <small>(optional)</small>
_[Boolean](http://docs.coronalabs.com/api/type/Boolean.html)._
Setting this value to true will result in cropping out the portion of
tiles that extend outside the pixel width/height.  In a full screen
application, this is not necessary.  Thus the default value for
this parameter is false.  This can be set to true when the
view control will not be the full screen.  However, setting this
to true does result in a performance hit.


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

tileEngineViewControl = TileEngine.ViewControl.new({
    parentGroup = sceneGroup,
    centerX = display.contentCenterX,
    centerY = display.contentCenterY,
    pixelWidth = display.actualContentWidth,
    pixelHeight = display.actualContentHeight,
    tileEngineInstance = tileEngineInstance
})
``````