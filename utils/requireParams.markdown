# Utils.requireParams()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Utils.*](lib_utils.markdown)
| __Return value__     | VOID
| __Keywords__         | 
| __See also__         | 


## Overview

This function verifies that the named properties have all been
defined on the passed in table.  It can be used to verify that
a function has been called with all of the required parameters.
If any of the parameters have not been defined, an error is thrown.

## Syntax

	Utils.requireParams( paramNames, params )

##### paramNames <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Table containing the names of required properties.

##### params <small>(optional)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Table containing the parameter values for the function.


## Examples

``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local Utils = TileEngine.Utils

-- Will throw an error.
local params1 = {
    x = 1
}
Utils.requireParams({"x", "y"}, params1)

-- Will not throw an error.
local params2 = {
    x = 1,
    y = 2
}
Utils.requireParams({"x", "y"}, params2)
``````