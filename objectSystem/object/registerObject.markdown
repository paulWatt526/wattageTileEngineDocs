# Object.registerObject()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.Object.*](type_object.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function is called when persisting an object graph to the DiskStream.
Any references managed by the class must be registered in this function.
**This function must call the super implementation first and continue
only if the call to super returns true.**

**NOTE: This function should be implemented by classes extending Object,
but it should not be called by the developer.  The ObjectSystem will
call this method internally.**

## Syntax

	Object.registerObject( diskStream )

##### diskStream <small>(required)</small>
_[DiskStream](../diskStream/type_diskStream)._
The stream used to write the file.

## Examples

Please see the example in the [Usage Guide](../usageGuide.markdown).