# gridline

A flexbox grid for responsive 12-column layouts. Set column widths, gaps, and offsets with CSS custom properties.

[![npm](https://img.shields.io/npm/v/gridline.svg?colorB=brightgreen)](https://www.npmjs.com/package/gridline)
[![NPM Downloads](https://img.shields.io/npm/dm/gridline.svg?style=flat)](https://www.npmjs.com/package/gridline)

[Demo](https://codepen.io/ux-ui/pen/QWzqdbp)

## Installation

```bash
npm install gridline
```

## Quick start

In an app with a bundler that handles CSS imports, import the stylesheet in your entry file:

```js
import 'gridline';
import './styles.css';
```

Add the grid to your page:

```html
<div class="gridline gridline--center">
  <section class="column">First column</section>
  <section class="column">Second column</section>
</div>
```

In `styles.css`, set the container width and give each column half the grid:

```css
body {
  margin: 0;
}

.gridline {
  --gridline-width: 1200px;
}

.column {
  --gridline-column: 6;
}
```

If you load styles through Sass, use the packaged CSS path instead of the JavaScript import:

```scss
@use "gridline/dist/index.css" as *;
```

## Classes

Add modifier classes alongside `.gridline`.

| Class | Effect |
| --- | --- |
| `.gridline` | Full-width flex container. |
| `.gridline--center` | Centers the container in the viewport. |
| `.gridline--left` | Aligns the container to the left edge of the layout. |
| `.gridline--right` | Aligns the container to the right edge of the layout. |
| `.gridline--scrolling` | Enables horizontal scrolling when the inner content overflows. Requires an inner scrolling block; see [Horizontal scrolling](#horizontal-scrolling). |
| `.gridline--collapse` | Removes the grid's flex layout and column sizing so children use normal document flow. |

## Styling

### CSS custom properties

| Variable | Set on | Default | Value |
| --- | --- | --- | --- |
| `--gridline-width` | `.gridline` | `100%` | Layout width, such as `1200px` or `100%`. |
| `--gridline-padding` | `.gridline` | `20px` | Outer space used in the layout calculation, such as `20px` or `2vw`. |
| `--gridline-gap` | `.gridline` | `20px` | Gap between columns. Use `0px` to remove it. |
| `--gridline-column` | Direct child | `12` | Column span; accepts integers or decimals. |
| `--gridline-offset` | Direct child | `0` | Offset to the right, in columns; accepts integers or decimals. |

Set these properties in your own selectors or inline on a column:

```html
<div class="gridline gridline--center">
  <section style="--gridline-column: 8; --gridline-offset: 2">
    An eight-column section with a two-column offset.
  </section>
</div>
```

### Extend a column to the viewport edge

With `.gridline--center`, `.gridline--left`, or `.gridline--right`, add `.edge` to a column to extend it toward the viewport edge. The first child extends left; a following child extends right. The selector matches any class name containing `edge`.

```html
<div class="gridline gridline--center">
  <section class="edge" style="--gridline-column: 6">Extends left</section>
  <section class="edge" style="--gridline-column: 6">Extends right</section>
</div>
```

### Horizontal scrolling

Use `.gridline--scrolling` on the outer container and `.scrolling` on an inner block. The inner selector also accepts class names containing `scrolling`.

With the stylesheet loaded as shown above:

```html
<div class="gridline gridline--scrolling">
  <div class="scrolling card-row">
    <article>First card</article>
    <article>Second card</article>
    <article>Third card</article>
  </div>
</div>
```

```css
.card-row {
  display: flex;
  gap: 20px;
  width: max-content;
}

.card-row > article {
  flex: 0 0 320px;
}
```

## License

MIT
