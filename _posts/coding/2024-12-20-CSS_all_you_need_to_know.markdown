---
layout: post
title:  "All You Need to Know About CSS: From Beginner to Advanced"
description: "A beginner friendly guide to CSS with coding samples."
date:   2024-12-20 5:22:29 -0600
categories: coding css web
---

CSS stands for **Cascading Style Sheets** and is the cornerstone of web development for styling web pages.

To understand the cascading aspect, there is a good article from [Amelia Wattenberger](https://2019.wattenberger.com/blog/css-cascade#level_1_3). In a nutshell the cascade is he way your browsers resolves competing CSS styles.

## Introduction to CSS

CSS is used to style HTML elements. It allows you to control colors, layouts, fonts, and more.

### Adding CSS to HTML

**Inline Styles:**

```html
<p style="color: red;">This is a red paragraph.</p>
```
This way is useful when you want to target only a single element. 

**Internal Stylesheet:**

```html
<!DOCTYPE html>
<html>
<head>
  <style>
    p { color: blue; }
  </style>
</head>
<body>
  <p>This is a blue paragraph.</p>
</body>
</html>
```

This way is useful when you want to target a single webpage. 

**External Stylesheet:**

```html
<!-- index.html -->
<link rel="stylesheet" href="styles.css">
```

```css
/* styles.css */
p { color: green; }
```
This is useful when you want to design a multipage website. 

---

## Selectors

Selectors target HTML elements to apply styles.

- **Universal Selector:**

```css
* { margin: 0; }
```

- **Type Selector:**

```css
h1 { color: purple; }
```

- **Class Selector:**

```css
.intro { font-size: 20px; }
```

- **ID Selector:**

```css
#main { background-color: yellow; }
```

- **Group Selector:**

```css
h1, p { text-align: center; }
```

### Combining Selectors

CSS allows combining selectors to target elements more precisely:

- **Descendant Selector:** Targets elements inside a parent:

```css
nav ul li {
  list-style: none;
}
```

- **Child Selector:** Targets direct children only:

```css
div > p {
  color: blue;
}
```

- **Adjacent Sibling Selector:** Targets the next immediate sibling:

```css
h1 + p {
  font-size: 18px;
}
```

- **General Sibling Selector:** Targets all siblings:

```css
h1 ~ p {
  color: gray;
}
```

## Colors and Units

- **Colors:** Named, HEX, RGB, HSL:
You can find matching colours on [Colorhunt](https://colorhunt.co/).
To convert RGB to HEX you can use [RGB Mixer](https://www.csfieldguide.org.nz/en/interactives/rgb-mixer/).

```css
body {
  background-color: #f0f0f0; /* Light grey */
  color: rgb(0, 0, 255); /* Blue */
}
```

- **Units:** px, %, em, rem:

```css
h1 { margin: 10px; font-size: 2em; }
```

## Box Model
The box model consists of margins, borders, padding, and the content itself. The `div` element acts like an invisible box to group content (in html).

```css
div {
  margin: 10px;
  border: 2px solid black;
  padding: 20px;
  width: 300px;
}
```

> 💡 **Tip:** Use the Chrome developer tool `command+option+i` in Chrome browser to inspect CSS and HTML properties of a website(css overview)!


## Positioning

- **Static (default):**

```css
p { position: static; }
```

- **Relative (relative to default position):**

```css
p { position: relative; top: 10px; }
```

- **Absolute (relative to nearest positioned ancestor or top left corner of webpage):**

```css
div { position: absolute; top: 50px; left: 100px; }
```

- **Fixed (relative to top left corner of browser window):**

```css
header { position: fixed; top: 0; }
```

- **z-index (Controls the stack order of elements. Higher values appear in front):**

```css
div {
  position: relative;
  z-index: 10;
}
```

## Responsive Design

- **Flexbox:**
Flexbox is used to define an overall page structure for one dimensiones layouts.

Per default the `flex-direction` is set to `row`. This means the main-axis is aligned horizontal from left to right and new items get added on the right side and until the row is full. If you set `flex-direction`to `column`, the main-axis turns from top to bottom.

**[Flexbox Cheat Sheet](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)**

```css
.container {
  display: flex;
  justify-content: space-around;
  align-items: center;
}
```

```html
<div class="container">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

- **Grid:**

Grid is used to define an overall page structure for two dimensiones layouts.
You can combine Flexbox and Grid.

**[Grid Cheat Sheet](https://css-tricks.com/snippets/css/complete-guide-grid/)**

```css
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 10px;
}
```

```html
<div class="grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

- **Media Queries for Layout Adjustments:**

The media rule is applied to define a different style for different kind of devices.
You can define `max-width` and `min-width` parameters and also combine them (`@media (min-width: 600px)and (max-width: 900px)`). More information can be found on [MDM Docs](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_media_queries/Using_media_queries).

```css
.container {
  display: flex;
  flex-wrap: wrap;
}
.item {
  flex: 1 1 300px;
}
@media (max-width: 768px) {
  .container {
    flex-direction: column;
  }
}
```

```html
<div class="container">
  <div class="item">Item 1</div>
  <div class="item">Item 2</div>
  <div class="item">Item 3</div>
</div>
```