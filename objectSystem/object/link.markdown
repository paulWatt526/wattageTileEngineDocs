# Object.link()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.*](../lib_objectSystem.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         | 


## Overview

This function is called when loading an object graph from the DiskStream.
This function works in conjunction with the load() and save() functions.
The save() function is responsible for saving properties as well as
saving the ID(s) of any referenced object(s).
The load() function is responsible for reading properties as well as
the previously saved ID(s) and registering a link using this old ID
with the DiskStream.
Finally, the link() function is responsible for getting the new object(s)
using the old ID(s) and recording a reference(s).
When a class manages a single or multiple references,
they must all be handled in these
three functions, and must be handled **in the same order.**  See the
example below for further clarification.
**This function must call the super implementation first.**

**NOTE: This function should be implemented by classes extending Object,
but it should not be called by the developer.  The ObjectSystem will
call this method internally.**

## Syntax

	Object.link( diskStream )

##### diskStream <small>(required)</small>
_[DiskStream](../diskStream/type_diskStream)._
The stream used to read the file.

## Examples

Please see the example in the
[Usage Guide](../usageGuide.markdown#Example).