# DiskStream.registerLink()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.*](../lib_objectSystem.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function works in conjunction with getNextLink() function.  This
function will register a reference link using the ID of the linked
object.  The function getNextLink() will retrieve the links in the same
order that they were passed into this function.

## Syntax

	DiskStream.registerLink( objectId )

##### objectId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The  ID of the referenced object.

## Examples

Please see the example in the [Usage Guide](../usageGuide.markdown).