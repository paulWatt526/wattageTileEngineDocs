# Engine.addModule()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine.*](type_engine.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function adds a module to the engine.


## Syntax

``````lua
Engine.addModule( params )
``````

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### module <small>(required)</small>
_[Module](../module/type_module.markdown)._ module to add to the engine.


## Examples

``````lua
engineInstance.addModule({
    module = moduleInstance
})
``````
