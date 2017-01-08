# TileLayer.new()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.TileLayer.*](type_tileLayer.markdown)
| __Return value__     | [TileLayer](type_tileLayer.markdown)
| __Keywords__         |
| __See also__         |


## Overview

This function creates a new instance of TileLayer.


## Syntax

	TileLayer.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### rows <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The rows in the layer.

##### columns <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The columns in the layer.


## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"

local tileLayer = TileEngine.TileLayer.new({
    rows = 100,
    columns = 100
})
``````