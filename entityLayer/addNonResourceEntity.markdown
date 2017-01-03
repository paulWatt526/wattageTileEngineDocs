# EntityLayer.addNonResourceEntity()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer](type_entityLayer.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html), [SpriteInfo](../spriteInfo/type_spriteInfo.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function adds display object directly to the layer.  This is useful
in cases where an entity needs to be added that the sprite resolver
cannot resolve.  The function will return an ID which can be used to
reference the resource and the SpriteInfo for the entity.


## Syntax

	EntityLayer.addNonResourceEntity( displayObject )

##### displayObject <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
Any display object.


## Examples

``````lua
local square = display.newRect(10, 10, 10, 10)
local id = entityLayerInstance.addNonResourceEntity(square)
``````
