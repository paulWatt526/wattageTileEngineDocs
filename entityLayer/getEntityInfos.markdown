# Engine.getEntityInfos()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns a table containing all of the SpriteInfo instances
for all of the resource entities.  The SpriteInfo instances are indexed
by their corresponding entity IDs.


## Syntax

``````lua
Engine.getEntityInfos()
``````

## Examples

``````lua
local spriteInfos = engineInstance.getEntityInfos()
local entitySpriteInfo = spriteInfos[42]
``````