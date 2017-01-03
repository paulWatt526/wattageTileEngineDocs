# Engine.getEntityInfo()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | [SpriteInfo](../spriteInfo/type_spriteInfo.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function returns the SpriteInfo instance for the given entity ID.


## Syntax

``````lua
Engine.getEntityInfo( id )
``````

##### id <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the entity to retrieve the info for.

## Examples

``````lua
local spriteInfo = engineInstance.getEntityInfo(42)
``````
