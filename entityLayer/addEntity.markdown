# EntityLayer.addEntity()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer.*](type_entityLayer.markdown)
| __Return value__     | [Number](https://docs.coronalabs.com/api/type/Number.html), [SpriteInfo](../spriteInfo/type_spriteInfo.markdown)
| __Keywords__         | 
| __See also__         | 


## Overview

This function adds an entity represented visually by the resource
associated with the specified key.  The key specified will be resolved
by the entity layer's sprite resolver.  The function will return an
ID which can be used to reference the resource and the SpriteInfo for
the entity.


## Syntax

	EntityLayer.addEntity( resourceKey )

##### resourceKey <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._ Key
to be resolved by the EntityLayer's SpriteResolver.


## Examples

``````lua
local id, spriteInfo = entityLayerInstance.addEntity("resourceKey")
``````
