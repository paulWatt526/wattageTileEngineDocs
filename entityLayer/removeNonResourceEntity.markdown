# Engine.removeNonResourceEntity()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer.*](type_entityLayer.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function removes the non-resource entity associated with specified ID.


## Syntax

``````lua
Engine.removeNonResourceEntity( id )
``````

##### id <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the non-resource entity to remove.

## Examples

``````lua
engineInstance.removeNonResourceEntity(42)
``````
