# SHPCSS
SHPCSS hopes to change the way we write stylesheets, by taking every web component and abstracting it to its simplest form. The idea is that every DOM node shares common properties, for example; almost everything has a size (width, height, padding etc) and colour (background, border, text etc). SHPCSS has broken these common properties into two core concepts: 'swatches' & 'shapes'.

Why? Because how many times have you typed out 'display: block; position: relative;' and then given that element a height, width, padding, margin etc? Probably many, many times. It should be easier than that, and less tedious. That's where 'shapes' come in. Each shape has predefined values that you can leave as default or override. Buttons, inputs, containers and list items are all just 'blocks'. Checkboxes are just squares, radios are circles, but your checkbox, radios, input and even your main website container may share many of the same properties, so even though they differ in size and shape, they can still share the same 'swatch' which may comprise of a white background and a grey 1px border. Once you've broken your website into swatches, you can pick and choose as you like.

No CSS overrides or duplicate properties!!

Our currently defined shapes are:

- Square
- Circle
- Rectangle
- Triangle

### Requirements
- Sass

### Installation

`npm install shpcss`

Include the library into your main SCSS project
`@import 'shpcss';`

### Usage

SHPCSS utilises a main mixin, `@include class()` and maps containing your swatches.

The `class()` mixin takes the following arguments:

- `$selector`: Your desired core selector
- `$shape`: The shape, as listed above
- `$variants`: A map of the variants (explained fully below)
- `$pseudo`: A map containing pseudo (::before and ::after) element properties

 


