[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg?style=flat-square)](https://www.webcomponents.org/element/leodido/matrix-layout)
 [![NPM](https://img.shields.io/npm/v/matrix-layout.svg?style=flat-square)](https://www.npmjs.com/package/matrix-layout) [![License](https://img.shields.io/badge/license-apache--2.0-yellowgreen.svg?style=flat-square)](http://opensource.org/licenses/Apache-2.0)

# \<matrix-layout\>

> A custom element and a style useful to create responsive and fluid grid layouts.

For this purpose this package provides a custom element - **matrix-layout** - and a shared style - **matrix-style**.

> The **matrix-layout** is an element wrapping and using **matrix-style** providing responsiveness and frameless mode for your [grid](https://material.io/guidelines/components/grid-lists.html#grid-lists-specs) layouts.

While ...

> The **matrix-style** is an helper style useful for creating your own [grid](https://material.io/guidelines/components/grid-lists.html#grid-lists-specs) layouts using CSS custom properties and CSS mixins it provides.

Because custom properties can be defined inside a `@media` rule, you can customize your grid layout for different **responsive breakpoints**.

Furthermore, since the only assumption it does is that you create a layout to use it, inserting within it some items in the light DOM it is completely decoupled from children elements.

It does not impose any constraint on child nodes.

So, you can use any element you want as child item.

See the [demo](/demo) directory to look at some implementations.

## Installation

One way to install it is executing `bower install leodido/matrix-layout --save` in your shell.

Or if you prefer `yarn add leodido/matrix-layout --save`, since it is published on [npm](https://www.npmjs.com/package/matrix-layout) registry also.

## Usage

Import `matrix-style.html` and include **matrix-style** in the style of an element's definition.

```html
<dom-module id="awesome-lattice">
    <template>
        <!-- Include the style to use the CSS mixins and the CSS variables it provides. -->
        <style include="matrix-style">
        </style>
    </template>
    <slot></slot>
</dom-module>
```

Then define the style details of your grid layout via **custom properties** and **mixin**.

```css
:host {
    --matrix-columns: 3;
    --matrix-gutter: 3px;
    --matrix-item-height: 30px;
    @apply --matrix-layout;
}
```

To all its slotted children will be applied the `--matrix-item` mixin.

So use can already use the `<awesome-lattice>` custom element.

```html
<awesome-lattice>
    <div>Awesome</div>
    <div>Wonderful</div>
    <div>Beautiful</div>
</awesome-lattice>
```

The [demo](/demo) directory contains more comprehensive examples.

### Expansible items

In many cases, it's useful to expand an item more than 1 column.

We call such type of items **wide items**.

To achieve this type of irregular grid layout, first you have to specify within the style of your custom element the number of columns that such items should expand to.

How? Setting the custom property `--matrix-wide-item-columns`.

```css
:host {
  --matrix-wide-item-columns: 3;
}
```

To indicate which item should expand, apply the **CSS mixin** `--matrix-wide-item` ...

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

Also in this case we provide more ways to accomplish this result.

In any case we first need to setup the aspect ratio.

```css
:host {
  --matrix-item-aspect-ratio: calc(16 / 9);
}
```

Then we can set the `has-aspect-ratio` **attribute** on our layout element to male **all** the elements respect it.

```html
<awesome-lattice has-aspect-ratio>
    ...
</awesome-lattice>
```

Another approach is to selectively define the items that have to respect the aspect ratio.

One way to do it is applying the **CSS mixin** - i.e., `--matrix-aspect-ratio-item` - to items we want to keep the choosen aspect ratio.

Otherwise simply use the `aspect-ratio` attribute on any item (in the light DOM) you want ...

This approaches are more flexible than the previous one since you can choose which items have to maintain the aspect ratio and which not.

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
