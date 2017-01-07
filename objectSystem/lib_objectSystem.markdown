# ObjectSystem

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [Library](http://docs.coronalabs.com/api/type/Library.html)
| __Corona Store__     | [wattageTileEngine](http://store.coronalabs.com/plugin/wattageTileEngine)
| __Keywords__         | Wattage, ObjectSystem, Tile Engine
| __See also__         |

## Overview

**NOTE: Use of this library is not necessary in order to use the tile
engine.  The tile engine uses this library internally and it has been
exposed for optional use by users of the tile engine.  This library
can be very useful in aiding with persisting object graphs but is an
advanced feature which requires some knowledge of object oriented
principles.  Please see the [Usage Guide](usageGuide.markdown)
and [Lua OOP Primer](../luaOopPrimer.markdown) for
additional details.  Again, use of this library is optional.**

## Guides

* [Usage Guide](usageGuide.markdown)
* [Lua OOP Primer](../luaOopPrimer.markdown)

## Syntax

	local TileEngine = require "plugin.wattageTileEngine"
	local ObjectSystem = TileEngine.ObjectSystem

### Types

The following types are exposed by this library:

* [ObjectSystem.Factory](factory/type_factory.markdown)
* [ObjectSystem.Object](object/type_object.markdown)
* [ObjectSystem.DiskStream](diskStream/type_diskStream.markdown)
