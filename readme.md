# InnovyzeTransportableJS

A library which can parse Transportable databases provided by Innovyze's InfoWorks and InfoNet/InfoAsset.

[Read more on the article about the library](http://sancarn.github.io/Business/Water/ICMTransportables)

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

Transportable database of this item. This parameter is only used to set parent_transportable property.

##### `item`

ZipItem found within a transportable database.

##### `data`

Data contained within ZipItem.


#### `id`
#### `data`
#### `isDeletedObject`
#### `isDir`
#### `isGlobal`
#### `isMapped`
#### `isModelObject`
#### `isModelObjectPart`
#### `isRootObject`
#### `meta`
#### `parent_transportable`
#### `zipItem`
#### `zipName`
#### `zipParentPath`
#### `zipPath`

#### `type`
#### `cumulative_id`
#### `child_ids`
#### `children`
#### `parent_id`
#### `parent`
#### `parts`
