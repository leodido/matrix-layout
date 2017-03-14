# \<matrix-layout>

[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg?style=flat-square)](https://www.webcomponents.org/element/leodido/matrix-layout)
 [![NPM](https://img.shields.io/npm/v/matrix-layout.svg?style=flat-square)](https://www.npmjs.com/package/matrix-layout) [![Bower](https://img.shields.io/bower/v/matrix-layout.svg?style=flat-square)](http://github.com/leodido/matrix-layout/releases/latest) [![License](https://img.shields.io/badge/license-apache--2.0-yellowgreen.svg?style=flat-square)](http://opensource.org/licenses/Apache-2.0)

This package contains two main components:

* A shared style component - i.e., **matrix-style**
* A custom element that uses it - i.e., **matrix-layout**

> The **matrix-layout** is an element wrapping and using **matrix-style** providing responsiveness and frameless mode for your grid layouts.

> The **matrix-style** is an helper style useful for creating fluid grid layouts using CSS custom properties and CSS mixins.

Because custom properties can be defined inside a `@media` rule, you can customize the matrix layout for different **responsive breakpoints**.

Furthermore, since the only assumption it does is that you create a layout to use it, inserting within it some items in the light DOM it is completely decoupled from children elements.

It does not impose any constraint on child nodes.

So, you can use any element you want as child item.

## Installation

You can install in many ways ...

One way is to execute `bower install leodido/matrix-layout --save` in your shell.

Or if you prefer `yarn add leodido/matrix-layout --save` ...

## Usage

Import `matrix-style.html` and include **matrix-style** in the style of an element's definition.

```html
<dom-module id="awesome-lattice">
    <template>
        <style include="matrix-style">
        </style>
    </template>

    <slot></slot>
</dom-module>
```

Then define the style details of your layout via **custom properties** and **mixin**.

```css
:host {
    --matrix-columns: 5;
    --matrix-gutter: 3px;
    --matrix-item-height: 30px;
    @apply --matrix-layout;
}
```

Finally use your `<awesome-lattice>` ...

```html
<awesome-lattice>
    <div>Awesome</div>
    <div>Wonderful</div>
    <div>Beautiful</div>
</awesome-lattice>
```

The **demo** directory contains more comprehensive examples.

### Expansible items

In many cases, it's useful to expand an item more than 1 column.

We call such type of items **wide items**.

To achieve this type of layout, you can specify within the style of your custom component the number of columns the such items should expand to by setting the custom property `--matrix-wide-item-columns`.

```css
:host {
  --matrix-wide-item-columns: 3;
}
```

To indicate which item should expand, apply the **CSS mixin** `--matrix-wide-item` to a rule with a selector to the item.

```css
:host ::slotted(.wide) {
  @apply(--matrix-wide-item);
}
```

This way you can also combine the expansibility of items with responsive breakpoints.

Otherwise simply use the provided **attribute** - i.e., `wide` - on the items in the light DOM.

```html
<awesome-lattice>
    <div wide>Extensible</div>
    <div>Awesome</div>
    <div>Wonderful</div>
    <div>Beautiful</div>
    <div>Hassle Free</div>
    <div wide>Layout</div>
    <div>Grid</div>
</awesome-lattice>
```

### Aspect ratio

Sometimes you want that your items maintain a given aspect ratio.

Also in this case we provide two ways to accomplish this result.

In any case we first need to setup the aspect ratio.

```css
:host {
  --matrix-item-aspect-ratio: calc(16 / 9);
}
```

Then we can set the `has-aspect-ratio` **attribute** on our layout element.

```html
<awesome-lattice has-aspect-ratio>
    ...
</awesome-lattice>
```

Otherwise we can apply the **CSS mixin** - i.e., `--matrix-aspect-ratio-item` - to items we want to keep the choosen aspect ratio.

Or also use the `aspect-ratio` attribute on any item we want to respect the defined aspect ratio.

So this approaches are more flexible since you can choose which items have to maintain the aspect ratio and which not.

### Styling

Custom property                             | Description                                                | Default
--------------------------------------------|------------------------------------------------------------|------------------
`--matrix-columns`                          | The number of columns per row.                             | 1
`--matrix-gutter`                           | The space between two items.                               | 0px
`--matrix-item-height`                      | The height of the items.                                   | auto
`--matrix-item-aspect-ratio`                | The aspect ratio of the items.                             | 1
`--matrix-wide-item-columns`                | The number of columns a wide item should expand to.        | 1

Mixin                                       | Description
--------------------------------------------|--------------------------------------------------------------------------
`--matrix-layout`                           | The styles to apply to the host we want to become a matrix layout.
`--matrix-item`                             | The styles to apply to each item.
`--matrix-wide-item`                        | The styles to apply to wide items (includes `--matrix-item`).
`--matrix-aspect-ratio-item`                | The styles to apply to items with aspect ratio (includes `--matrix-item`).
`--matrix-without-space-around`             | The styles to apply to the container within the layout to remove side spaces from it.

---

[![Analytics](https://ga-beacon.appspot.com/UA-49657176-1/matrix-layout?flat)](https://github.com/igrigorik/ga-beacon)