# DiskStream.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.*](../lib_objectSystem.markdown)
| __Return value__     | [DiskStream](type_diskStream)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of type DiskStream.  DiskStream
contains functions that assist in saving and loading an object graph.


## Syntax

	DiskStream.new()

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local DiskStream = TileEngine.ObjectSystem.DiskStream

local diskStreamInstance = DiskStream.new()
``````
