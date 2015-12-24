# react-blockly-component

A React component that embeds a [Blockly](https://developers.google.com/blockly/) visual programming editor.

Features:

* Supports an `xmlDidChange` prop so other components can easily consume the XML generated by the editor
* Generates the toolbox XML from a `toolboxCategories` or `toolboxBlocks` prop, and automatically notifies Blockly when it's been updated

## Building

Clone this repository, and then inside it, do:

```bash
npm install
npm run build
```

You'll get a `dist` directory containing the compiled JS file and a source map.

## Properties

All properties are optional except where otherwise specified.

* `initialXml`: The XML of the program to initially load in the editor.
* `workspaceConfiguration`: Any configuration options to be passed into `Blockly.inject` (except for `toolbox`, which is handled automatically).
* `wrapperDivClassName`: The value for the `class` attribute to be used on the `<div>` elements generated by this component.  Typically you'll need to use this to set the height of the Blockly editor, using either an explicit `height` style, flexboxes, or some other means.
* `toolboxCategories`: An array of categories for the toolbox.  Each category is an object including the following properties:
  * `name`: The display name of this category.
  * `custom`: The value for the `custom` attribute of this category (can be either `"VARIABLE"` or `"PROCEDURE"`).
  * `categories`: An array of subcategories, each of which follows the same format as this object.
  * `blocks`: An array of blocks to appear in the category.  Each block is an object including the following properties:
    * `type` (required): The Blockly type name for the block (such as `"controls_if"` or `"logic_compare"`).
    * `shadow`: True if this is a shadow block; false or undefined otherwise.
    * `fields`: An object mapping from field names to pre-set values for those fields.
    * `values`: An object mapping from value input names to pre-set connected blocks for those value inputs.  Each block is an object following the same format as this one.
    * `statements`: An object mapping from statement input names to pre-set connected blocks for those statement inputs.  Each block is an object following the same format as this one.
    * `next`: The next block connected to this one, which is an object following the same format as this one.
    * `mutation`: An object specifying the content of the `<mutation>` tag for this block, with the following properties:
      * `attributes`: An object mapping from attribute names to values for those attributes.
      * `innerContent`: The XML content of the `<mutation>` tag in string format.
* `toolboxBlocks`: An array of top-level blocks for the toolbox.  Each block is an object following the format of the objects in the `toolboxCategories` `blocks` array (specified above).  If this property is defined, `toolboxCategories` should not be defined, since Blockly's toolbox can either contain blocks or categories, but not both.
* `xmlDidChange`: A callback function that will be called whenever the XML content generated by the Blockly editor changes.  The new XML content will be passed as an argument to the function.
* `processToolboxCategory`: A callback function that can be used to pre-process the content of a toolbox category.  This function is passed a single object from the `toolboxCategories` array and is expected to return an object of the same format.  This is useful if another React component is embedding `BlocklyEditor` and wants to add dynamic content to the toolbox.

## Example usage

See `public/index.html` for a fairly full-fledged demo that shows off most of the features of this component.

## Contributing

We accept pull requests and issues!  You can file an issue on this project, or fork, modify, and file a pull request.

Please note that this project is released with a Contributor Code of Conduct. By participating in this project you agree to abide by its terms.

## Licensing

react-blockly-component is Copyright &copy; 2015 PatientsLikeMe, Inc.  Distributed under the terms and conditions of the MIT License.