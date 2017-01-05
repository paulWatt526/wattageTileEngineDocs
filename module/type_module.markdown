# Module

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Module](type_module.markdown)
| __Corona Store__     | [wattageTileEngine](http://store.coronalabs.com/plugin/wattageTileEngine)
| __Keywords__         | Wattage, Module, Tile Engine
| __See also__         |

## Overview

A module represents a collection of layers, lighting model, and line
of sight model.  The engine may contain a number of modules, but only
one module can be active at any time.  This allows switching between
environments in the engine.  Modules can all be loaded at once, or
on-demand as needed.

The use case for loading modules all at once is
when it is necessary to switch between these modules quickly.  For
example, it may be necessary to have separate modules for each floor
within a building.  Each floor would need its own set of layers and
its own lighting model, and switching between floors should not take
too much time.

The use case for loading modules on-demand is when modules are
particularly large and switching between them will not occur too
frequently.

## Syntax

	local TileEngine = require "plugin.wattageTileEngine"
	local ModuleType = TileEngine.Module

### Constructor

##### [Module.new()](new.markdown)

### Functions

##### [Module.insertLayerAtIndex()](insertLayerAtIndex.markdown)
##### [Module.addPhysicsBody()](addPhysicsBody.markdown)
##### [Module.removePhysicsBody()](removePhysicsBody.markdown)
##### [Module.hasDirtyTile()](hasDirtyTile.markdown)
##### [Module.activate()](activate.markdown)
##### [Module.deactivate()](deactivate.markdown)
##### [Module.destroy()](destroy.markdown)
