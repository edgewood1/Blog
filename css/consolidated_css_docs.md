# A Comprehensive Guide to CSS

This document provides a consolidated overview of CSS, covering fundamental concepts, layout techniques, styling, responsive design, and advanced topics.

## 1. CSS Fundamentals

### 1.1. Style Rules

A CSS rule consists of a selector and a declaration block.

```css
/* The entire block is a "rule" */
.my-class { /* This is the "selector" */
  /* This is a "declaration" */
  color: red;
  /* "property": "value" */
  font-size: 16px;
}
```

### 1.2. Selectors & Combinators

Selectors target the HTML elements you want to style.

-   **Type/Element**: `h1`, `p`
-   **Class**: `.my-class`
-   **ID**: `#my-id`
-   **Attribute**: `a[title]`, `input[type="text"]`
-   **Pseudo-class**: `:hover`, `:focus`
-   **Pseudo-element**: `::before`, `::after`

**Attribute Selector Examples:**

```css
/* Selects <a> elements with a title attribute */
a[title] {
  color: purple;
}

/* Selects <a> elements where href exactly matches */
a[href="https://example.org"] {
  color: green;
}

/* Selects <a> elements where href contains "example" */
a[href*="example"] {
  font-size: 2em;
}

/* Selects <a> elements whose class attribute contains the word "logo" */
a[class~="logo"] {
  padding: 2px;
}

/* Selects inputs of type username OR password */
input[type="username"], input[type="password"] {
    color: blue;
}
```

**Combinators** define the relationship between selectors:

-   **Descendant (` `)**: `div p` - Selects all `<p>` elements inside `<div>` elements.
-   **Child (`>` بينا** `div > p` - Selects all `<p>` elements that are *direct children* of a `<div>`.
-   **Adjacent Sibling (`+`)**: `div + p` - Selects the first `<p>` element placed *immediately after* a `<div>`.
-   **General Sibling (`~`)**: `div ~ p` - Selects all `<p>` elements that are siblings of and appear after a `<div>`.

### 1.3. Specificity

Specificity determines which CSS rule is applied by the browser when multiple rules conflict. The hierarchy is:

1.  **Inline styles** (e.g., `style="color: red;"`)
2.  **ID selectors** (`#example`)
3.  **Class selectors** (`.example`), attribute selectors (`[type="radio"]`), and pseudo-classes (`:hover`)
4.  **Type selectors** (`h1`) and pseudo-elements (`::before`)

The universal selector (`*`), combinators (`+`, `>`, `~`), and the negation pseudo-class (`:not()`) themselves have no effect on specificity.

### 1.4. The Box Model

Every HTML element is a rectangular box. Its total size is determined by four properties:

-   **Content**: The text, image, or other content. Its size is set by `width` and `height`.
-   **Padding**: The space between the content and the border.
-   **Border**: A line that goes around the padding and content.
-   **Margin**: The space outside the border, creating a gap between elements.

**Shorthand:** `padding` and `margin` can be specified with 1, 2, 3, or 4 values, corresponding to `top`, `right`, `bottom`, and `left` in a clockwise direction.

To center a block-level element horizontally, give it a `width` and set `margin: 0 auto;`.

### 1.5. CSS Units

-   **`px` (Pixels)**: Fixed-size units, not ideal for scaling.
-   **`pt` (Points)**: Fixed-size units, mainly for print. 1pt = 1/72 inch.
-   **`%` (Percentage)**: Relative to the parent element's property.
-   **`em`**: Relative to the `font-size` of the *current element*. `2em` means 2 times the current font size.
-   **`rem` (Root em)**: Relative to the `font-size` of the *root element* (`<html>`). This provides a consistent reference for scaling across the entire application.
-   **`vw` (Viewport Width)**: 1% of the viewport's width.
-   **`vh` (Viewport Height)**: 1% of the viewport's height.

### 1.6. Colors

-   **Hexadecimal (`#RRGGBB`)**: `#0000ff` is blue.
-   **RGB (`rgb(red, green, blue)`)**: `rgb(0, 0, 255)` is blue. `rgba()` adds an alpha (transparency) channel.
-   **HSL (`hsl(hue, saturation, lightness)`)**: More intuitive for creating color variations.
    -   `hue`: The color pigment, on a 360-degree wheel.
    -   `saturation`: The intensity, from `0%` (gray) to `100%` (full color).
    -   `lightness`: The brightness, from `0%` (black) to `100%` (white).
    -   `hsla()` adds an alpha channel: `hsl(200deg 100% 50% / 0.5)`.

## 2. Layout Techniques

### 2.1. The `display` Property

-   **`block`**: Starts on a new line and takes up the full width available. `width` and `height` are respected. (e.g., `<div>`, `<p>`, `<h1>`).
-   **`inline`**: Flows with text, does not start on a new line, and only takes up as much width as necessary. `width` and `height` have no effect. (e.g., `<span>`, `<a>`, `<strong>`).
-   **`inline-block`**: Flows with text like an `inline` element, but `width` and `height` are respected like a `block` element.
-   **`none`**: Hides the element and removes it from the document flow entirely.
-   **`flex`**: Enables Flexbox layout.
-   **`grid`**: Enables Grid layout.

### 2.2. Positioning

The `position` property, along with `top`, `right`, `bottom`, and `left`, allows you to move elements out of the normal document flow.

-   **`static`**: The default value. The element is in the normal document flow.
-   **`relative`**: The element is positioned relative to its normal position. The space it would have occupied is preserved.
-   **`absolute`**: The element is removed from the normal flow and positioned relative to its nearest *positioned* ancestor. If none exists, it uses the document body.
-   **`fixed`**: The element is positioned relative to the viewport. It stays in the same place even when the page is scrolled.
-   **`sticky`**: A hybrid of `relative` and `fixed`. It acts as `relative` until the user scrolls to a certain point, at which point it "sticks" and behaves like `fixed`.

### 2.3. Flexbox

A one-dimensional layout model for arranging items in rows or columns.

-   **`display: flex`**: Applied to the container element.
-   **`flex-direction`**: `row` (default) or `column`.
-   **`justify-content`**: Aligns items along the main axis (horizontally if `row`).
-   **`align-items`**: Aligns items along the cross axis (vertically if `row`).

For flex items (the children):
-   **`flex-grow`**: Dictates how much of the remaining space the item should take up.
-   **`flex-shrink`**: Dictates how much an item should shrink if there isn't enough space.
-   **`flex-basis`**: The default size of an item before the remaining space is distributed.

### 2.4. Grid

A two-dimensional layout model for arranging items in rows and columns.

-   **`display: grid`**: Applied to the container element.
-   **`grid-template-columns` / `grid-template-rows`**: Defines the size and number of columns and rows. You can use `fr` units to define a fraction of the available space.
    ```css
    .container {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 10px;
    }
    ```
-   **`grid-template-areas`**: Allows you to name grid areas and create a visual layout in your CSS.
-   **`gap`**: Shorthand for `row-gap` and `column-gap`.

### 2.5. Stacking Context & `z-index`

A stacking context is a three-dimensional conceptualization of HTML elements along the z-axis (perpendicular to the screen). Within a stacking context, the `z-index` property determines the stacking order of elements.

A new stacking context is formed by, among other things:
-   The root `<html>` element.
-   An element with `position: absolute` or `relative` and a `z-index` other than `auto`.
-   An element with `position: fixed` or `sticky`.
-   An element with an `opacity` less than 1.
-   An element with a `transform`, `filter`, or `perspective` property.

Within a stacking context, the order is (from bottom to top):
1.  The background and borders of the element forming the context.
2.  Positioned elements with negative `z-index`.
3.  Non-positioned elements (in order of appearance).
4.  Positioned elements with `z-index: auto` or `0`.
5.  Positioned elements with positive `z-index`.

### 2.6. Handling Overflow

The `overflow` property controls what happens when a child's content is larger than its parent container.

-   **`visible`** (default): Content renders outside the parent's box.
-   **`hidden`**: Content is clipped and the rest is invisible.
-   **`scroll`**: Content is clipped and a scrollbar is added to see the rest.
-   **`auto`**: A scrollbar is added only if content overflows.

## 3. Visual Styling

### 3.1. Typography

-   **`font-family`**: A prioritized list of fonts (a "font stack") for the browser to try.
-   **`font-size`**: The size of the text. Use `rem` units for scalability.
-   **`font-weight`**: The thickness of the font (`normal`, `bold`, or a numeric value).
-   **`font-style`**: `normal`, `italic`.
-   **`text-decoration`**: `none`, `underline`, `overline`, `line-through`.
-   **`text-align`**: `left`, `right`, `center`, `justify`.
-   **`letter-spacing`**: Adjusts the space between characters.
-   **`line-height`**: Adjusts the vertical distance between lines of text. A unitless value (e.g., `1.5`) is recommended.

### 3.2. Transforms, Transitions, and Animations

-   **`transform`**: Modifies the coordinate space of an element. Functions include:
    -   `translate(x, y)`: Moves the element.
    -   `scale(x, y)`: Resizes the element.
    -   `rotate(angle)`: Rotates the element.
    -   `skew(x-angle, y-angle)`: Skews the element.
-   **`transition`**: Creates a smooth animation between an element's old and new states.
    ```css
    .box {
      transition: transform 250ms ease-in-out, opacity 500ms;
    }
    ```
-   **`@keyframes`**: Defines the steps of an animation sequence, which can then be applied to an element using the `animation` property.

## 4. Responsive Design

### 4.1. Viewports

The viewport is the user's visible area of a web page.
-   **`Element.clientWidth`**: An element's content and padding width.
-   **`window.innerWidth`**: The browser viewport width, including the vertical scrollbar.

### 4.2. Media Queries

Media queries apply CSS rules only when certain conditions are met, such as the viewport width. This is the foundation of responsive design.

```css
/* Base styles (mobile-first) */
.container {
  width: 100%;
}

/* Tablet styles */
@media (min-width: 768px) {
  .container {
    width: 750px;
  }
}

/* Desktop styles */
@media (min-width: 992px) {
  .container {
    width: 970px;
  }
}
```

## 5. Advanced CSS and Pre-processors

### 5.1. CSS Custom Properties (Variables)

Custom properties allow you to define reusable values. They are subject to the cascade and can be updated with JavaScript.

```css
:root {
  --main-color: #4f4f4f;
  --base-font-size: 1rem;
}

body {
  color: var(--main-color);
  font-size: var(--base-font-size);
}
```

### 5.2. Sass/SCSS and Less

These are CSS pre-processors that add features like variables, nesting, mixins, and functions. The code is compiled into regular CSS that browsers can understand.

-   **SCSS (`.scss`)**: Superset of CSS. All valid CSS is valid SCSS.
-   **Sass (`.sass`)**: Older syntax that uses indentation instead of brackets and newlines instead of semicolons.
-   **Less**: Similar to SCSS, uses `@` for variables.

**Example (SCSS Nesting):**
```scss
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
  }
}
```

### 5.3. Styling Shadow DOM (`::part`)

The `::part` pseudo-element makes it possible to style specific elements inside a shadow tree from outside the shadow DOM.

```javascript
// Inside a web component's shadow DOM
<div id="main" part="test">Hello</div>
```

```css
/* In the page's global stylesheet */
my-component::part(test) {
  background-color: green;
}
```

## 6. CSS in JavaScript

### 6.1. `getComputedStyle()`

A JavaScript method that returns an object containing the values of all CSS properties of an element after applying active stylesheets and resolving any basic computation.

```javascript
const elem = document.getElementById('my-element');
const style = window.getComputedStyle(elem);
const width = style.width;
```

### 6.2. `clsx`

A tiny utility for constructing `className` strings conditionally. It's useful in JavaScript frameworks like React.

```javascript
import clsx from 'clsx';

// In a component...
const classes = clsx('base-class', {
  'is-active': props.isActive,
  'is-disabled': props.isDisabled
});

return <div className={classes}>...</div>;
```
