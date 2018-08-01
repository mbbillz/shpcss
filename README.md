# 🔺◼️ SHPCSS 🔺◼️

A simpler way to write SCSS.

- Rapidly develop DRY, modular and scalable stylesheets.
- Define a single 'source of truth' for all of your website's styles for easier maintainability
- Quickly generate element variants - perfect for BEMs and theming
- Ensures that your codebase is DRY and organised
- Change an element's properties with one line
- Decouple styles from selectors
- Little to no need to manually write CSS
- Includes a bunch of useful mixins for alignment, positioning etc (WIP)
- No duplicate CSS properties

> **IMPORTANT:** This project is currently just a **CONCEPT** and is not ready for production. Suggestions and contributions welcomed!

SHPCSS hopes to simplify and speed up the creation of stylesheets by taking every web component and abstracting it to its simplest form. The idea is that every DOM node shares common properties, for example; almost everything has a size (width, height, padding etc) and colour (background, border, text etc). SHPCSS has broken these common properties into two core concepts: `swatches` & `shapes`.


### Simple usage
Define a map containing `swatches`:

```
$swatches: (
  'a': (
    border: solid 2px darken($secondary, 5%),
    color: $secondary,
    text-transform: uppercase,
    font-weight: bold,
    'hover': (
      color: $ui-a,
      background-color: $secondary,
    )
  ),
);
```

Include the main `class()` mixin:

```
@include class(
  $selector: '.swatch',
  $shape: 'block',
  $base: (
    'width': auto,
    'custom': (
      padding: 1rem 1.5rem
    )
  ),
  $variants: (
    '--a': (
      'interactive': true,
      'swatch': map-get($swatches, 'a')
    )
  )
);
```

SHPCSS will output:

```
.swatch {
  position: relative;
  background: none;
  border: none;
  box-sizing: border-box;
  width: auto;
  padding: 1rem 1.5rem;
}
.swatch--a {
  border: solid 2px #2912ad;
  color: #2e14c4;
  text-transform: uppercase;
  font-weight: bold;
}
.swatch--a:hover {
  cursor: pointer;
  outline: none;
  color: #fff;
  background-color: #2e14c4;
}
```

### About
Every time you define a new class, it's likely that you're going to give that class some baseline properties, such as display, position, width, height etc, why not be able to just specify that it's a `block`? I have created these mixins so you can simply create a new `block` or `square` or `circle` and the rest is generated for you. The shapes contain predefined values that you can leave as default or override. For example, buttons, inputs, containers and list items are all conceptually `blocks`, so just define them as such let SHPCSS handle the build. 

Once you've done this, you'll want to apply a `swatch`. You've defined your checkboxes as squares, radios as circles and your main container as a block, but you recognise that actually they are all stylistically similar and despite being different shapes, they can still share the same `swatch` which may comprise of a white background, some padding and a grey 1px border. Simply apply that swatch and you're done.

Once you've broken your website into swatches, you can pick and choose as you like and easily and quickly mix and match by changing very little code. You can also quickly generate interactivity, pseudo elements, variants (great for use with BEMs or similar conventions), aligned elements and much more!

### Current features
- Class generator
- Variant generator
- Square
- Block
- Interactive swatches
- Pseudo elements
- Built in check to ensure output contains no duplicate properties

### To do
- Circle
- Triangle
- More inbuilt functions/mixins
- Better documentation
- A proper demo!

### Requirements
- Sass

### Installation
`npm install shpcss`

Include the library into your main SCSS project:
`@import 'shpcss';`

### Usage
SHPCSS utilises a main mixin, `@include class()` and maps containing your swatches. The `class()` mixin takes the following arguments:

| Arg | Optional | Type | Description | Value |
|:-|:-|:-|:-|:-|
| `$selector`| false | String | Your desired core selector | `.selector`, `#id`, `tag` |
| `$shape` | false | String | The shape | `block`, `square` |
| `$reset` | false | String | Apply a reset/normalise to this element | `body`, `list` |
| `$base` | true | Object | A map containing base properties | See below |
| `$variants` | true | Object | A map containing variant properties | See below |
| `$pseudo` | true | Object | A map containing pseudo (::before and ::after) element properties | null | See below |

##### Base map
The properties you pass in your base map will vary depending on the shape but there are some shared properties you can use
###### Shared properties
These properties can be used for all shapes

| Property | Optional | Type | Description | Value |
|:-|:-|:-|:-|:-|
| `swatch`| true | Object | Apply a swatch to the current element | map with swatch styles e.g `map-get($swatches, 'swatch-a')` |
| `align`| true | String | Align the current element | `center`, `center-x`, `center-y` |
| `children`| true | String | Align the current element's children | `center`, `center-x`, or a flex value e.g `space-between` |

###### Square properties
If you're using a square:

| Property | Optional | Type | Description | Value |
|:-|:-|:-|:-|:-|
| `size`| true | Number | Your desired square size | value and unit e.g `10px`, `2rem` |

###### Block properties
If you're using a block:

| Property | Optional | Type | Description | Value |
|:-|:-|:-|:-|:-|
| `width`| true | Number | Your desired block width | e.g `100%`, `auto` |
| `height`| true | Number | Your desired block height | value and unit e.g `10px`, `2rem` |


