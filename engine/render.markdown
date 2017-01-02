# Engine.render()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function renders the visible tiles using the supplied camera.


## Syntax

``````lua
Engine.render( camera )
``````

##### camera <small>(required)</small>
_[Camera](../camera/type_camera.markdown)._
The camera used to render the tiles.  The camera configuration will
determine which tiles are currently visible and only those tile will
be processed.

## Examples

``````lua
engineInstance.render(cameraInstance)
``````