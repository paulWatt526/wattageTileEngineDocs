# Factory

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Factory](type_Factory.markdown)
| __Corona Store__     | [wattageTileEngine](http://store.coronalabs.com/plugin/wattageTileEngine)
| __Keywords__         |
| __See also__         |

## Overview

The factory is used by the object system to create new instances of
registered types.  It is only used when loading object graphs from the
disk stream.  In order for an object to support persistence to disk, a
constructor must be registered with the factory for that objects type.

A single instance is utilized by the object system, so this is implemented
as a static class.

## Syntax

	local TileEngine = require "plugin.wattageTileEngine"
	local ObjectFactory = TileEngine.ObjectSystem.Factory

### Functions

##### [Factory.registerForType()](registerForType.markdown)

##### [Factory.getForType()](getForType.markdown)