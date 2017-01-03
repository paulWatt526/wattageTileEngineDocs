# LightingModel.updateLight()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.EntityLayer](type_entityLayer.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will update the location of the light associated with the
specified ID.

**NOTE: If the new position of the light is the same as the old
position, the light will not be marked dirty and will not result in
further processing.**

## Syntax

	LightingModel.updateLight( params )

##### params <small>(required)</small>
_[Table](http://docs.coronalabs.com/api/type/Table.html)._
Contains all required inputs. See **Required Properties** below.

### Required Properties

The `params` table contains the following properties:
##### lightId <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The ID of the light to move.

##### newRow <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
 The row of the destination tile.

 **NOTE: Row numbers start at 1 and increase from top to bottom.**

##### newColumn <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The column of the destination tile.

**NOTE: Column numbers start at 1 and increase from left to right.**

## Examples

``````lua
lightingModelInstance.updateLight({
    lightId = 42,
    newRow = 10,
    newColumn = 15
})
``````
