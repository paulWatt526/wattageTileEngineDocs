# EntityLayer.destroy()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer.*](type_entityLayer.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function releses all resources held by the instance.  Once this
method is called, the instance is no longer of any use and any
references to it should be cleared.

**NOTE: This is used internally.**

## Syntax

	EntityLayer.destroy()

## Examples

``````lua
entityLayerInstance.destory()
``````