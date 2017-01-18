# Object System Usage Guide

The object system provides a system to manage the persistence of complex
object graphs.  It does this both by providing an abstract base class which
can be extended to add persistence capabilities to an object graph, and by
providing tools to aid in writing and reading to file.  It
is by no means required in order to use the tile engine but has been
exposed as part of the library since the Wattage Tile Engine uses this
object system internally.

This guide contains three main sections:

* [Extending the Abstract Object Base Class](#extending-the-abstract-object-base-class)
* [Saving and Loading an Object Graph](#saving-and-loading-an-object-graph)
* [Example](#example)

## Extending the Abstract Object Base Class

The following steps should be followed when extending the abstract
Object class:

1. Extend the Object Class
2. Override Object.registerObject() If Necessary
3. Override Object.save()
4. Override Object.load()
5. Override Object.link() If Necessary.
6. Register the Type with the Factory.

These steps are detailed in the following sections.

**NOTE: If you have not done so already, please review the "Lua OOP Primer" for
details on the approach this library has taken to OOP in lua.**

### Extend the Object Class

When creating the "self" reference in your class, it should be done as
follows to extend Object:

``````lua
local MyType = {}
MyType.new = function()
    local self = Object.new({objectType="myTypeName"})

    return self
end
``````

### Override Object.registerObject() If Necessary

If your class contains member references to other objects, then your
class must override Object.registerObject() to register those references.
**When overriding this function, you must first make a call to the super
implementation and continue only if that call returns true.** This is
necessary to prevent duplicate registrations.  The call to the super
implementation will return false if this instance has already been
registered (it is possible that many objects in the graph may reference
this instance and only one registration is needed).

Member references are registered by passing the diskStream to their
registerObject() functions.

``````lua
local parentRegisterObject = self.registerObject
function self.registerObject(diskStream)
    if not parentRegisterObject(diskStream) then
        return false
    end

    -- register member references
    reference.registerObject(diskStream)
end
``````

### Override Object.save()

Implement save() to write out properties (like numbers and strings) and
to write out the object IDs of any references.  **When overriding this
function, you must first make a call to the super implementation.  Also,
make note of the order that properties and references are written
because they must be read in the same order.**

Values are written using DiskStream.write()

``````lua
local parentSave = self.save
function self.save(diskStream)
    parentSave(diskStream)

    -- write properties
    diskStream.write(property1)
    diskStream.write(property2)

    -- write references
    diskStream.write(reference1.getObjectId())
    diskStream.write(reference2.getObjectId())
end
``````

### Override Object.load()

Implement load() to read the properties and object IDs that were written
by save().  Then register links for the object IDs so that the link()
function can finalize those links after all objects have been loaded.
**When overriding this function, you must first make a call
to the super implementation.  Also, make note of the order that
references are read because they must be read in the same order that
they were written in.  The links must also be registered in the same
order that they will be finalized in the link() function.**


``````lua
local parentLoad = self.load
function self.load(diskStream)
    parentLoad(diskStream)

    -- read properties
    property1 = diskStream.read()
    property2 = diskStream.read()

    -- read references
    local reference1Id = diskStream.read()
    diskStream.registerLink(reference1Id)

    local reference2Id = diskStream.read()
    diskStream.registerLink(reference2Id)
end
``````


### Override Object.link() If Necessary

If your class contains member references to other objects, then your
class must override Object.link() to finalize links to references to matching
loaded instances.  It will do so by retrieving the link registered in
the load function and querying the DiskStream for the new object.
**When overriding this function, you must first make
a call to the super implementation.  Also, when finalizing the link,
pay close attention to the order.  It must match the order that the
links were registered in the load() function.**


``````lua
local parentLink = self.link
function self.link(diskStream)
    parentLink(diskStream)

    reference1 = diskStream.getNewObjectForOldId(diskStream.getNextLink())
    reference2 = diskStream.getNewObjectForOldId(diskStream.getNextLink())
end
``````

### Register the Type with the Factory

Finally, the type must be registered with the Factory.  This tells the
ObjectSystem how to create an instance of this type.

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local ObjectFactory = TileEngine.ObjectSystem.Factory

ObjectFactory.registerForType("myTypeName", MyType.new)
``````

## Saving and Loading an Object Graph

Saving and loading is performed using DiskStream functions saveToFile()
and loadFromFile().

### FileStream.saveToFile()

When saving your object graph, you need to pass
the top level Object into the saveToFile() function.  The top level
object should not be referenced by any other object in the graph.

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local DiskStream = TileEngine.ObjectSystem.DiskStream


...Object graph created here...


local streamInstance = DiskStream.new()
streamInstance.saveToFile(topLevelInstance, "dataFile.dat")

``````

### FileStream.loadFromFile()

Loading the object graph from file is done as follows:

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local DiskStream = TileEngine.ObjectSystem.DiskStream

local streamInstance = DiskStream.new()
local topLevelInstance = streamInstance.loadFromFile("dataFile.dat")

...Use object graph here...

``````

## Example

This example creates an object graph representing a company which
has both a reference to a country and a collection of employees.  Each
employee also has an optional reference to a project.  The relationships
can be seen in the following diagram:

![Class diagram of example object graph](objGraphClassDiagram.png)

Granted, this is a fairly simple example and could easily be persisted
using a flattened table, and if the object graph
in your application is this simple, that is how it should be persisted.
However, object graphs can get pretty complex, and it can become
difficult to persist all of the relationships in a complex graph.
That is the situation where the object system is most useful.  The
example, detailed below has been chosen because it illustrates a number
of key scenarios:

* Saving and loading properties
    * The property "name" is persisted in CountryClass (and others).
* Saving and loading references
    * Multiple types of references to show importance of order across
    functions.
        * CompanyClass has a non-nullable reference of type CountryClass and
        a collection of EmployeeClass references.  They are handled in
        the same order within save(), load(), and link().
    * A collection of references.
        * CompanyClass has a collection of EmployeeClass type references.
    * Optional (Nullable) references.
        * EmployeeClass has a nullable reference of type ProjectClass.

``````lua
local TileEngine = require "plugin.wattageTileEngine"
local DiskStream = TileEngine.ObjectSystem.DiskStream
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

        -- write properties
        diskStream.write(name)
    end

    local parentLoad = self.load
    function self.load(diskStream)
        parentLoad(diskStream)

        -- read properties
        name = diskStream.read()
    end

    return self
end
ObjectFactory.registerForType(CountryClass.objectType, CountryClass.new)


local CompanyClass = {}
CompanyClass.objectType = "Company"
CompanyClass.new = function(params)
    Utils.requireParams({
        "name",
        "country"
    }, params)

    local country = params.country
    local employees = {}
    local name = params.name

    local self = Object.new({objectType=CompanyClass.objectType})

    function self.getCountry()
        return country
    end

    function self.getName()
        return name
    end

    function self.addEmployee(employee)
        table.insert(employees, employee)
    end

    function self.getEmployeeNames()
        local names = {}
        for i=1,#employees do
            table.insert(names, employees[i].getName())
        end
        return names
    end

    function self.getEmployeeCount()
        return #employees
    end

    local parentRegisterObject = self.registerObject
    function self.registerObject(diskStream)
        if not parentRegisterObject(diskStream) then
            return false
        end

        country.registerObject(diskStream)

        for i=1,#employees do
            employees[i].registerObject(diskStream)
        end
    end

    local parentSave = self.save
    function self.save(diskStream)
        parentSave(diskStream)

        -- write properties
        diskStream.write(name)

        -- write references

        -- write country
        diskStream.write(country.getObjectId())

        -- first write count of employee references
        diskStream.write(#employees)

        -- now write the IDs of employee references
        for i=1,#employees do
            diskStream.write(employees[i].getObjectId()
        end
    end

    local parentLoad = self.load
    function self.load(diskStream)
        parentLoad(diskStream)

        -- read properties
        name = diskStream.read()

        -- read references

        -- read country
        local countryObjectId = diskStream.read()
        diskStream.registerLink(countryObjectId)

        -- first read count of employee references
        self._employeeCount = diskStream.read()

        -- new read IDs of employee references and register a link for each
        for i=1,self._employeeCount do
            local objectId = diskStream.read()
            diskStream.registerLink(objectId)
        end
    end

    local parentLink = self.link
    function self.link(diskStream)
        parentLink(diskStream)

        -- link country
        country = diskStream.getNewObjectForOldId(diskStream.getNextLink())

        -- link employees
        for i=1,self._employeeCount do
            table.insert(employees, diskStream.getNewObjectForOldId(diskStream.getNextLink())
        end
        self._employeeCount = nil
    end

    return self
end
ObjectFactory.registerForType(CompanyClass.objectType, CompanyClass.new)


local ProjectClass = {}
local ProjectClass.objectType = "Project"
ProjectClass.new = function(params)
    Utils.requireParams({
        "name"
    }, params)

    local name = params.name

    local self = Object.new({objectType=ProjectClass.objectType})

    function self.getName()
        return name
    end

    local parentSave = self.save
    function self.save(diskStream)
        parentSave(diskStream)

        -- write properties
        diskStream.write(name)
    end

    local parentLoad = self.load
    function self.load(diskStream)
        parentLoad(diskStream)

        -- read properties
        name = diskStream.read()
    end

    return self
end
ObjectFactory.registerForType(ProjectClass.objectType, ProjectClass.new)


local EmployeeClass = {}
EmployeeClass.objectType = "Employee"
EmployeeClass.new = function(params)
    Utils.requireParams({
        "name"
    }, params)

    local name = params.name
    local project

    local self = Object.new({objectType=EmployeeClass.objectType})

    function self.getName()
        return name
    end

    function self.getProject()
        return project
    end

    function self.setProject(projectParam)
        project = projectParam
    end

    local parentRegisterObject = self.registerObject
    function self.registerObject(diskStream)
        if not parentRegisterObject(diskStream) then
            return false
        end

        if project ~= nil then
            project.registerObject(diskStream)
        end
    end

    local parentSave = self.save
    function self.save(diskStream)
        parentSave(diskStream)

        -- write properties
        diskStream.write(name)

        -- write references
        if project ~= nil then
            diskStream.write(project.getObjectId())
        else
            diskStream.write("NULL")
        end
    end

    local parentLoad = self.load
    function self.load(diskStream)
        parentLoad(diskStream)

        -- read properties
        name = diskStream.read()

        -- read references
        self._projectValue = diskStream.read()
        if self._projectValue ~= "NULL" then
            diskStream.registerLink(self._projectValue)
        end
    end

    local parentLink = self.link
    function self.link(diskStream)
        parentLink(diskStream)

        if self._projectValue ~= "NULL" then
            project = diskStream.getNewObjectForOldId(diskStream.getNextLink())
        else
            project = nil
        end
        self._projectValue = nil
    end

    return self
end
ObjectFactory.registerForType(EmployeeClass.objectType, EmployeeClass.new)



local countryUSA = CountryClass.new({
    name = "USA"
})

local techCompany = CompanyClass.new({
    name = "TechCo",
    country = countryUSA
})

local searchProject = ProjectClass.new({
    name = "Super Search"
})
local socialProject = ProjectClass.new({
    name = "Text Me"
})

local fred = EmployeeClass.new({
    name = "Fred"
})
fred.setProject(searchProject)

local george = EmployeeClass.new({
    name = "George"
})
george.setProject(socialProject)

local deadWeight = EmployeeClass.new({
    name = "DeadWeight"
})

techCompany.addEmployee(fred)
techCompany.addEmployee(george)
techCompany.addEmployee(deadWeight)

local diskStream = DiskStream.new()
diskStream.saveToFile(techCompany, "techCompany.dat")

local techCompanyLoadedFromFile = diskStream.loadFromFile( "techCompany.dat")
``````