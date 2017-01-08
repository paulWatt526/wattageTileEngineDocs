# DiskStream.getNewObjectForOldId()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.DiskStream.*](type_diskStream.markdown)
| __Return value__     | [Object](../object/type_object.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function is will return an object loaded from file which
had the specified ID when it was persisted.

**NOTE: The object will have a new ID which will not necessarily
be the same ID it had when it was saved.**

## Syntax

	DiskStream.getNewObjectForOldId( oldObjectId )

##### oldObjectId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID the object had when it was persisted.

## Examples

Please see the example in the
[Usage Guide](../usageGuide.markdown).