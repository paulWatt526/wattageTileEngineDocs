# Engine.removeModule()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | [module](../module/type_module.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function removes a module from the engine and returns the removed
module.


## Syntax

``````lua
Engine.removeModule( params )
``````

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### moduleName <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._ name of module to remove.


## Examples

``````lua
engineInstance.removeModule({
    moduleName = "myModule"
})
``````
