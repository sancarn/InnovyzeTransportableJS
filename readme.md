# InnovyzeTransportableJS

A library which can parse Transportable databases provided by Innovyze's InfoWorks and InfoNet/InfoAsset.

[Read more on the article about the library](http://sancarn.github.io/Business/Water/ICMTransportables)

## Disclaimer

Note: This library is unofficial and will be unsupported by Innovyze.

## Dependencies:

### Always required

* JSZip

### Required ifs:

* If you want to use this library in the browser and require databases by path.
** JSZipUtil is required.
* If you want to use `toJsTree()` or `toFileViewer()`.
** JSTree is required.


## How to use:

After including the library you can simply instantiate a transportable as follows:

```js
const transportable = new Transportable("./libs/Transportable Examples/Validations.icmt");
transportable.onLoad(function(){
  //do stuff with transportable
});
```

Alternatively:

```js
const transportable = new Transportable(fileObject);
transportable.onLoad(function(){
  //do stuff with transportable
});
```

At this point simply explore the database API.

## API

### `Transportable` properties and methods:

#### `global`

This object contains data from the `Globals.dat` file.

##### `GUID`

The Globally Unique Identifier for this database.

##### `SubVersion`

The SubVersion is used, from what I gather, to identify the schema used for the Model Network database. 

##### `VersionGUID`

The version GUID is used by ICM to determine whether or not the transportable database should be opened in ICM.

#### `root`

The root `TransportableItem` which has been instantiated from the `RootObjects.Dat` file.

#### `items`

All `TransportableItem` objects contained within the database.

#### `loaded`

Whether the transportable database has loaded or not.

#### `_parsedZip`

The zip object created by JSZip which InnovyzeTransportableJS uses to parse the database.

#### `toTreeViewer(element,options)`

Display the transportable database as a JsTree. See [example](...) here. Returns a jsTree object.

##### `element`

Either a CSS selector, HTML element or JQuery object of the element which will contain the JsTree.

##### `options`

Object containing options.

```
stripes        - jsTree stripes theme.
wholerow       - jsTree whole row plugin.
include-upload - Currently work in progress. The idea is to 
                 include an upload button to allow refreshing
                 of the transportable viewer.
```

#### `treeViewerInfo`

Object containing information about the instanciated Tree Viewer if there is one.

##### `element`

The `element` object passed to the `toTreeViewer()` function.

##### `items`

An array of `TransportableItem` objects displayed in the tree. Note this array is not the same as `transportable.items`.

##### `jstree`

The `jstree` object for the tree viewer.

##### `options`

The options passed to `toTreeViewer()`

##### `transportable`

The `Transportable` object which instantiated the tree viewer.

##### `tree`

The root element of the tree displayed in the tree viewer.



#### `toFileViewer(element,options)`

##### `element`

Either a CSS selector, HTML element or JQuery object of the element which will contain the JsTree.

##### `options`

Object containing options.

```
stripes - jsTree stripes theme.
```

#### `fileViewerInfo`

Object containing information about the instanciated File Viewer if there is one.

##### `element`

The `element` object passed to the `toFileViewer()` function.

##### `items`

An array of `TransportableItem` objects displayed in the tree. Note this array is not the same as `transportable.items`.

##### `jstree`

The `jstree` object for the file viewer.

##### `options`

The options passed to `toFileViewer()`

##### `transportable`

The `Transportable` object which instantiated the file viewer.

##### `tree`

The root element of the tree displayed in the file viewer.

### `TransportableItem`

#### `constructor(transportable,item,data)`

##### `transportable`

Type: `Transportable`. Transportable database of this item. This parameter is only used to set parent_transportable property.

##### `item`

Type: `ZipItem`. JSZip ZipItem found within a transportable database.

##### `data`

Type: `String`. Data contained within ZipItem.

#### `id`

Type: `Int`. Contains the id of a `TransportableItem` object. `id` can also be set to:

```
 0 : Root Object
-1 : Global object
-2 : Unmapped object (unknown data)
```

ID is calculated using the type iid and the cumulative id (integer found at the end of the file name). This id is used to determine the tree structure.

#### `isDeletedObject`

Type: `Boolean`. Determines whether the zip item is assumed to be a deleted object. This occurs when the ID is like:

* AG**XXX**1.DAT
* AG**XXX**2.DAT
* MODG**XXX**3.DAT

#### `isDir`

Type: `Boolean`. Determines whether the zip item is a folder or not

#### `isGlobal`

Type: `Boolean`. Determines whether the zip item is the `Globals.Dat` file.

#### `isRootObject`

Type: `Boolean`. Determines whether the zip item is the `RootObjects.Dat` file.

#### `isModelObject`

Type: `Boolean`. Determines whether the zip item is assumed to be a model object. I.E. has file pattern:

* AG1.DAT
* AG2.DAT
* AG3.DAT
* `/[A-Z]+\d+\.DAT/i`

#### `isModelObjectPart`

Type: `Boolean`. Determines whether the zip item is assumed to be related to a model object. I.E. has file pattern:

* AG1SomePart.DAT
* AG1SomeOtherPart.something
* `/[A-Z]+\d+\w+/i`

#### `isMapped`

Type: `Boolean`. Determines whether the zip item has been mapped to a model object, part or else.

#### `parent_transportable`

Type: `Transportable`. The transportable object which contains this item.

#### `zipItem`

Type: `ZipItem`. The ZipItem created by JSZip which represents a specific file within the zip archive.

#### `zipName`

Type: `String`. Name of item in the zip archive.

#### `zipParentPath`

Type: `String`. Path of parent in the zip archive.

#### `zipPath`

Type: `String`. Path of item in the zip archive.


#### `meta`

Type: `Object`. If the item is a model object this will contain all data found within the `.DAT` file as a comma seperated. Objects data is found by the name in the `.DAT` file. Also worth noting arrays of integers are converted to actual arrays of integers.

#### `type`

Type: `Object`. If the item is a model object this will contain the type information of the item.

#### `cumulative_id`

Type: `Int`. If the item is a model object this will contain the cumulative id used to calculate the id.

#### `child_ids`

Type: `Array`. If the item is a model object this will contain an array of children ids contained within this model object.

#### `children`

Type: `Array`. If the item is a model object this will contain an array of children contained within this model object.

#### `parent_id`

Type: `Int`. If the item is a model object this will contain the id of this item's parent.

#### `parent`

Type: `TransportableItem`. If the item is a model object this will contain the `TransportableItem` which corresponds to this item's parent.

#### `parts`

Type: `Array`. If the item is a model object this will contain all identified part's which correspond to this `TransportableItem`, if applicable.
