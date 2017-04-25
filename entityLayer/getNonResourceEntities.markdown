# Engine.getNonResourceEntities()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer.*](type_entityLayer.markdown)
| __Return value__     | [Table](http://docs.coronalabs.com/api/type/Table.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns a table containing all of the DisplayObjects
for all of the non-resource entities.  The DisplayObjects are indexed
by their corresponding entity IDs.


## Syntax

``````lua
Engine.getNonResourceEntities()
``````

## Examples

``````lua
local sprites = engineInstance.getNonResourceEntities()
local entitySprite = sprites[42]
``````