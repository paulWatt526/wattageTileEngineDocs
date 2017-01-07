# DiskStream

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [DiskStream](type_diskStream.markdown)
| __Corona Store__     | [wattageTileEngine](http://store.coronalabs.com/plugin/wattageTileEngine)
| __Keywords__         |
| __See also__         |

## Overview
This class is used to save and load object graphs built using the
ObjectSystem.

## Syntax

	local TileEngine = require "plugin.wattageTileEngine"
	local DiskStream = TileEngine.ObjectSystem.DiskStream

### Constructor

##### [DiskStream.new()](new.markdown)

### Functions

##### [DiskStream.saveToFile()](saveToFile.markdown)

##### [DiskStream.loadFromFile()](loadFromFile.markdown)

##### [DiskStream.write()](write.markdown)

##### [DiskStream.read()](read.markdown)

##### [DiskStream.getNewObjectForOldId()](getNewObjectForOldId.markdown)

##### [DiskStream.registerLink()](registerLink.markdown)

##### [DiskStream.getNextLink()](getNextLink.markdown)