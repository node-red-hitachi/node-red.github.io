---
layout: docs-api
toc: toc-api-ui.html
title: TypedInput Widget
slug:
  - url: "/docs/api/ui"
    label: "ui widgets"
  - 'typedinput'
---

A replacement for a regular `<input>` that allows the type of the value to be
chosen, including options for string, number and boolean types.

<div class="widget">
    <div class="col-4-12">
        <h3>Options</h3>
        <table>
            <tr><td><a href="#options-default">default</a></td></tr>
            <tr><td><a href="#options-types">types</a></td></tr>
            <tr><td><a href="#options-typeField">typeField</a></td></tr>
        </table>
    </div>
    <div class="col-4-12">
        <h3>Methods</h3>
        <table>
            <tr><td><a href="#methods-disable">disable</a></td></tr>
            <tr><td><a href="#methods-disabled-get">disabled</a></td></tr>           
            <tr><td><a href="#methods-hide">hide</a></td></tr>
            <tr><td><a href="#methods-show">show</a></td></tr>
            <tr><td><a href="#methods-type">type</a></td></tr>
            <tr><td><a href="#methods-types">types</a></td></tr>
            <tr><td><a href="#methods-validate">validate</a></td></tr>
            <tr><td><a href="#methods-value">value</a></td></tr>
            <tr><td><a href="#methods-width">width</a></td></tr>
        </table>
    </div>
    <div class="col-4-12">
    <h3>Events</h3>
    <table>
    <tr><td><a href="#events-change">change</a></td></tr>
    </table>
    <h3>Types</h3>
    <table>
    <tr><td><a href="#types-typedefinition">TypeDefinition</a></td></tr>
    </table>
    </div>
</div>


### Options

#### <a href="#options-default" name="options-default">default</a>

<span class="method-return">Type: String</span>

If defined, sets the default type of the input if [`typeField`](#options-typeField)
is not set.

```javascript
$(".input").typedInput({
    default: "msg"
});
```

#### <a href="#options-types" name="options-types">types</a>

<span class="method-return">Type: Array</span>

Sets the list of types the element will offer.

The value of the option is an array of string-identifiers for the
predefined types and [TypeDefinition](#types-typedefinition) objects for any custom types.

The predefined types are:

identifier | description
-----------|------------
`msg` | a `msg.` property expression
`flow` | a `flow.` property expression
`global` | a `global.` property expression
`str` | a String
`num` | a Number
`bool` | a Boolean
`json` | a valid JSON string
`bin` | a Node.js Buffer
`re` | a Regular Expression
`jsonata` | a Jsonata Expression
`date` | the current timestamp
`env` | an environment variable
`node` | a `node.` property expression
`cred` | a secure credential

```javascript
$(".input").typedInput({
    types: ["msg","str"]
});
```

#### <a href="#options-typeField" name="options-typeField">typeField</a>

<span class="method-return">Type: CSS Selector</span>

In some circumstances it is desirable to already have an `<input>` element to store
the type value of the typedInput. This option allows such an existing element to be
provided. As the type of the typedInput is changed, the value of the provided input
will also change.

```javascript
$(".input").typedInput({
    typeField: ".my-type-field"
});
```

### Methods

<a name="methods-type"></a>

#### <a href="#methods-disable" name="methods-disable">disable()</a>

*Since Node-RED 1.2.7*

Disable the typedInput when it is currently enabled.

```javascript
$(".input").typedInput('disable');
```

#### <a href="#methods-disabled-get" name="methods-disabled-get">disabled()</a>

*Since Node-RED 1.2.7*

<span class="method-return">Returns: Boolean</span>

Gets whether the typedInput is currently disabled or not.

```javascript
$(".input").typedInput('disabled');
```

#### <a href="#methods-hide" name="methods-hide">hide()</a>

Hide the typedInput when it is currently visible.

```javascript
$(".input").typedInput('hide');
```

#### <a href="#methods-show" name="methods-show">show()</a>

Show the typedInput when it is currently hidden.

```javascript
$(".input").typedInput('show');
```

#### <a href="#methods-type-get" name="methods-type-get">type()</a>

<span class="method-return">Returns: String</span>

Gets the selected type of the typedInput.

```javascript
var type = $(".input").typedInput('type');
```

#### <a href="#methods-type-set" name="methods-type-set">type( type )</a>

Sets the selected type of the typedInput.

```javascript
$(".input").typedInput('type','msg');
```

#### <a href="#methods-types" name="methods-types">types( types )</a>

Sets the list of types offered by the typedInput. See the description of the [`types` option](#options-types).

```javascript
$(".input").typedInput('types',['str','num']);
```

#### <a href="#methods-validate" name="methods-validate">validate()</a>

<span class="method-return">Returns: Boolean</span>

Triggers a revalidation of the typedInput's type/value. This occurs automatically
whenever the type or value change, but this method allows it to be run manually.

```javascript
var isValid = $(".input").typedInput('validate');
```

<a name="methods-value"></a>

#### <a href="#methods-value-get" name="methods-value-get">value()</a>

<span class="method-return">Returns: String</span>

Gets the value of the typedInput.

```javascript
var value = $(".input").typedInput('value');
```

#### <a href="#methods-value-set" name="methods-value-set">value( value )</a>

Sets the value of the typedInput.

```javascript
$(".input").typedInput('value','payload');
```

#### <a href="#methods-width" name="methods-width">width( width )</a>

Sets the width of the typedInput. This must be used in place of the standard
`jQuery.width()` function as it ensures the component resizes properly.

```javascript
$(".input").typedInput('width', '200px');
```

### Events

#### <a href="#events-change" name="events-change">change( event, type, value )</a>

Triggered when either the type or value of the input is changed.

```javascript
$(".input").on('change', function(type, value) {} );
```

*Note:* The `value` property was added in Node-RED 1.3

### Types

#### <a href="#types-typedefinition" name="types-typedefinition">TypeDefinition</a>

A `TypeDefinition` object describes a type that can be offered by a typedInput
element.

It is an object with the following properties:

Property | Type    | Required | Description
---------|---------|----------|-------------
`value`  | string  | yes      | The identifier for the type
`label`  | string  |          | A label to display in the type menu
`icon`   | string  |          | An icon to display in the type menu
`options`| array   |          | If the type has a fixed set of values, this is an array of string options for the value. For example, `["true","false"]` for the boolean type.
`hasValue`|boolean |          | Set to `false` if there is no value associated with the type.
`validate`|function|          | A function to validate the value for the type.

##### Examples

Number type:

```javascript
{
    value:"num",
    label:"number",
    icon:"red/images/typedInput/09.png",
    validate:/^[+-]?[0-9]*\.?[0-9]*([eE][-+]?[0-9]+)?$/
}
```

Boolean type:

```javascript
{
    value:"bool",
    label:"boolean",
    icon:"red/images/typedInput/bool.png",
    options:["true","false"]
}
```

Timestamp type:

```javascript
{
    value:"date",
    label:"timestamp",
    hasValue:false
}
```


<style>

.widget h3 {
    margin-left: 0;
    padding-bottom: 5px;
    border-bottom: 2px solid #B68181;
}
.widget:after {
    content:"";
    display:block;
    clear:both;
}
.method-return {
    float: right;
    font-style: italic;
    padding-left: 10px;
    border-left: 2px solid #B68181;
}
</style>
