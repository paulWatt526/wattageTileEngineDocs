# Lua Object-Oriented Programming (OOP) Primer

## Overview
There are a number of ways to practice OOP in Lua, and a quick internet
search will reveal them.  This document focuses on the approach
utilized by the internal components of the Wattage Tile Engine, which
uses closures.  Although it is not necessary to use OOP in order
to use the Wattage Tile Engine, it is necessary to understand these
concepts in order to use the optional ObjectSystem which this library
exposes.  For more information on the ObjectSystem, please see the
[ObjectSystem Usage Guide](objectSystem/usageGuide.markdown).

This guide will show how the following can be implemented using the
closure approach for OOP.

* [Class Definition](#class-definition)
* [Public Properties](#public-properties)
* [Private Variables](#private-variables)
* [Public Functions](#public-functions)
* [Private Functions](#private-functions)
* [Static Functions](#static-functions)
* [Inheritance](#inheritance)
* [Function Overriding](#function-overriding)
* [Abstract Function](#abstract-function)

## Class Definition

Each class exposes a new() function which acts as a constructor and
creates the closure.  The new function will create an instance  and
return that instance.  In the following example, that instance is
called "self"...

``````lua
-- Create the table for the class definition
local EmptyClassDefinition = {}

-- Define the new() function
EmptyClassDefinition.new = function()
    local self = {}
    return self
end
``````

## Public Properties

Public properties can be created by declaring them on "self".  See
the example below...

``````lua
local ExampleClass = {}
ExampleClass.new = function()
    local self = {}

    self.publicProperty = 42

    return self
end

local instance = ExampleClass.new()

-- Prints 42
print(instance.publicProperty)
``````

## Private Variables

Private properties can be created by declaring local variables within
the closure...

``````lua
local ExampleClass = {}
ExampleClass.new = function()
    local self = {}

    local privateProperty = "secret"

    return self
end

local instance = ExampleClass.new()

-- Prints nil
print(instance.privateProperty)
``````

## Public Functions

Public functions can be created by declaring them on "self".  See the
example below where we add a public function as an accessor for
the private property...

``````lua
local ExampleClass = {}
ExampleClass.new = function()
    local self = {}

    local privateProperty = "secret"

    function self.getPrivateProperty()
        return privateProperty
    end

    return self
end

local instance = ExampleClass.new()

-- Prints "secret"
print(instance.getPrivateProperty())
``````

## Private Functions

Private functions can be created by declaring local functions within
the closure.  These private functions would be in scope within public
functions but not outside the closure.  See the following example...

``````lua
local ExampleClass = {}
ExampleClass.new = function()
    local self = {}

    local function privateFunction()
        print("Inside Private Function")
    end

    function self.publicFunction()
        print("Inside Public and Calling Private")
        privateFunction()
    end

    return self
end

local instance = ExampleClass.new()

-- Prints the following...
-- "Inside Public and Calling Private"
-- "Inside Private Function"
instance.publicFunction()

-- This results in an error...
instance.privateFunction()
``````

## Static Functions

A static function can be created by declaring it on the class definition
table.  See the following example...

``````lua
-- Create the table for the class definition
local ExampleClassDefinition = {}

ExampleClassDefinition.staticFunction()
    print("Inside Static Function")
end

-- Define the new() function
ExampleClassDefinition.new = function()
    local self = {}
    return self
end

-- Prints "Inside Static Function"
ExampleClassDefinition.staticFunction()
``````

## Inheritance

A class may inherit another class by instantiating the parent class
as the "self" instance.  Consider the following example...

``````lua
local BaseClass = {}
BaseClass.new = function()
    local self = {}

    function self.baseFunction()
        print("Inside the baseFunction")
    end

    return self
end

local ExtendingClass = {}
ExtendingClass.new = function()
    local self = BaseClass.new()

    return self
end

local extendingClassInstance = ExtendingClass.new()

-- Prints "Inside the baseFunction"
extendingClassInstance.baseFunction()
``````

## Function Overriding

A class may override a function on its parent class by overwriting the
function reference on "self".  A call to the parent class implementation
can be facilitated by making a private copy of the parent implementation
before overriding it.  See ExtendingClass1 and ExtendingClass2 in the
example below...

``````lua
local BaseClass = {}
BaseClass.new = function()
    local self = {}

    function self.baseFunction()
        print("Inside the baseFunction")
    end

    return self
end

local ExtendingClass1 = {}
ExtendingClass1.new = function()
    local self = BaseClass.new()

    function self.baseFunction()
        print("Inside Overriding Function")
    end

    return self
end

local ExtendingClass2 = {}
ExtendingClass2.new = function()
    local self = BaseClass.new()

    local parentBaseFunction = self.baseFunction
    function self.baseFunction()
        parentBaseFunction()
        print("Inside Overriding Function")
    end

    return self
end

local extendingClass1Instance = ExtendingClass1.new()
-- Prints "Inside Overriding Function"
extendingClass1Instance.baseFunction()

local extendingClass2Instance = ExtendingClass2.new()
-- Prints the following...
-- "Inside the baseFunction"
-- "Inside Overriding Function"
extendingClass2Instance.baseFunction()
``````

## Abstract Function

Abstract functions can be simulated by declaring functions which
throw an error if they are not overridden.  Consider the following
example...

``````lua
local BaseClass = {}
BaseClass.new = function()
    local self = {}

    function self.baseFunction()
        error("I am abstract!")
    end

    return self
end

local ExtendingClass1 = {}
ExtendingClass1.new = function()
    local self = BaseClass.new()

    return self
end

local ExtendingClass2 = {}
ExtendingClass2.new = function()
    local self = BaseClass.new()

    function self.baseFunction()
        print("Inside Overriding Function")
    end

    return self
end

local extendingClass1Instance = ExtendingClass1.new()
-- Results in the error "I am abstract!"
extendingClass1Instance.baseFunction()

local extendingClass2Instance = ExtendingClass2.new()
-- Prints the following...
-- "Inside Overriding Function"
extendingClass2Instance.baseFunction()
``````