# Module.removePhysicsBody()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Module.*](type_module.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function removes a physics body from the module.  After a physics
body is removed from the module, the physics body is no longer under the
modules management.  Activating/deactivating the module will no longer
activate/deactivate the physics object.


## Syntax

	Module.removePhysicsBody( physicsBody )

##### physicsBody <small>(required)</small>
_[DisplayObject](https://docs.coronalabs.com/api/type/DisplayObject/index.html)._
The physics body to remove.


## Examples

``````lua
moduleInstance.removePhysicsBody(physicsBody)
``````
