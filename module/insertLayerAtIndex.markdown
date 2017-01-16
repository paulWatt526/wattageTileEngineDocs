# Module.insertLayerAtIndex()

|                      | &nbsp;
| -------------------- | ---------------------------------------------------------------
| __Type__             | [function](http://docs.coronalabs.com/api/type/Function.html)
| __Library__          | [wattageTileEngine.Module.*](type_module.markdown)
| __Return value__     | VOID
| __Keywords__         |
| __See also__         |


## Overview

This function will insert a layer in the module at the given index.  If
a layer already exists at the specified index, then the new layer will
be inserted and all existing layers at that index or higher will be
shifted one index higher.

When adding a layer, a scaling delta may be specified.  This scaling
delta indicates the difference in scaling from the layer with the next
lower index.


## Syntax

	Module.insertLayerAtIndex( layer, index, scalingDelta, xScrollCoefficient, yScrollCoefficient )

##### layer <small>(required)</small>
_Layer._
The layer to add.  This may be any layer type including the following:

* [TileLayer](../tileLayer/type_tileLayer.markdown)
* [EntityLayer](../entityLayer/type_entityLayer.markdown)

##### index <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The index to insert at.

##### scalingDelta <small>(required)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The difference in scaling between this layer and the layer before it.

##### xScrollCoefficient <small>(optional)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The coefficient applied to camera X position.  This can be used to
implement parallax scrolling.  A value greater than 1 makes this
scroll faster than the camera.  A value smaller than 1 makes this
scroll slower than the camera.  The default value is 1 which results
in a speed which matches the camera.

##### yScrollCoefficient <small>(optional)</small>
_[Number](https://docs.coronalabs.com/api/type/Number.html)._
The coefficient applied to camera Y position.  This can be used to
implement parallax scrolling.  A value greater than 1 makes this
scroll faster than the camera.  A value smaller than 1 makes this
scroll slower than the camera.  The default value is 1 which results
in a speed which matches the camera.

## Examples

``````lua
moduleInstance.insertLayerAtIndex( myLayer, 3, 0.05 )
``````
