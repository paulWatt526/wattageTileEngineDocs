# Engine.setActiveModule()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Engine](type_engine.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function sets the active module in the engine.  This will deactivate
the currently active module (if there is one).


## Syntax

``````lua
Engine.setActiveModule( params )
``````

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### moduleName <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._ name of module to make
active.


## Examples

``````lua
engineInstance.setActiveModule({
    moduleName = "myModule"
})
``````