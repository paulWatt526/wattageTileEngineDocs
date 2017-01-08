# Object.new()

|                      | &nbsp; 
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.ObjectSystem.Object.*](type_object.markdown)
| __Return value__     | [Object](type_object)
| __Keywords__         | 
| __See also__         | 


## Overview

This function creates a new instance of type Object.  This class should
be considered an abstract class and should not be instantiated.  Instead
it should be extended by classes that will participate in the ObjectSystem.


## Syntax

	Object.new( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.


### Required Properties

The `params` table contains the following properties:

##### objectType <small>(required)</small>
_[String](https://docs.coronalabs.com/api/type/String.html)._
The type name of the object.

## Examples

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local ObjectFactory = TileEngine.ObjectSystem.Factory
local Object = TileEngine.ObjectSystem.Object
local Utils = TileEngine.Utils

local CountryClass = {}
CountryClass.objectType = "Country"
CountryClass.new = function(params)
    Utils.requireParams({
        "name"
    }, params)

    local name = params.name

    local self = Object.new({objectType=CompanyClass.objectType})

    function self.getName()
        return name
    end

    local parentSave = self.save
    function self.save(diskStream)
        parentSave(diskStream)

        // write properties
        diskStream.write(name)
    end

    local parentLoad = self.load
    function self.load(diskStream)
        parentLoad(diskStream)

        // read properties
        name = diskStream.read()
    end

    return self
end
ObjectFactory.registerForType(CountryClass.objectType, CountryClass.new)
``````
