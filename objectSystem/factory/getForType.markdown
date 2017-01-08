# Factory.getForType()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.Factory.*](type_factory.markdown)
| __Return value__     | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Keywords__         |
| __See also__         |


## Overview

This function returns the registered constructor for the specified
type.

**NOTE: This function is used internally by the object system.**


## Syntax

	Factory.getForType( typeName, factoryMethod )

##### typeName <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
Name of the type.

## Examples

``````lua
local TileEngine = require 'plugin.wattageTileEngine'
local Object = TileEngine.ObjectSystem.Object
local ObjectFactory = TileEngine.ObjectSystem.Factory

local AnimalClass = {}
AnimalClass.new = function(nameParam)
    local self = Object.new({objectType="Animal"})

    local name = nameParam

    function self.sayName()
        print("Hello, my name is " .. name)
    end

    return self
end
ObjectFactory.registerForType("Animal", AnimalClass.new)

local animalNamedFred = ObjectFactory.getForType("Animal")("Fred")
``````
