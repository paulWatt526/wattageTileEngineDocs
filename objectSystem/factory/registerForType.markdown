# Factory.registerForType()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.Factory.*](type_factory.markdown)
| __Return value__     | VOID
| __Keywords__         | 
| __See also__         | 


## Overview

This function registers a constructor for a given type.  This is
necessary in order to support object graph persistence.


## Syntax

	Factory.registerForType( typeName, factoryMethod )

##### typeName <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
Name of the type.

##### factoryMethod <small>(required)</small>
_[function](http://docs.coronalabs.com/api/type/Function.html)._
Method to use for creating new instances of the type.


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
``````
