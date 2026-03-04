# Technical Paper on HTML/CSS

## Box Model

### What is Box Model?

In CSS, every HTML element is treated as a **box**.
The **Box Model** describes the space around and inside that box.

### Parts of Box Model

1. **Content** – The actual text or image inside the element
2. **Padding** – Space between content and border
3. **Border** – The edge around the padding
4. **Margin** – Space outside the border

### Structure

```
Margin
 └── Border
      └── Padding
           └── Content
```

### Example

```html
<div class="box">Hello</div>
```

```css
.box {
  width: 200px;
  padding: 20px;
  border: 2px solid black;
  margin: 30px;
}
```



---

# Inline vs Block Elements

## Block Elements

### What are Block Elements?

Block elements take **full width of the page** and always start on a **new line**.

### Examples

* `<div>`
* `<p>`
* `<h1>` to `<h6>`
* `<section>`

### Example

```html
<div>First Div</div>
<div>Second Div</div>
```

Output:
The second div appears **below** the first div.



---

## Inline Elements

### What are Inline Elements?

Inline elements take **only the space they need** and stay in the **same line**.

### Examples

* `<span>`
* `<a>`
* `<strong>`
* `<em>`

### Example

```html
<span>Hello</span>
<span>World</span>
```

Output:
Both words appear **in the same line**.



---

# CSS Positioning

## Position: Relative

### What is Relative Position?

`position: relative` moves an element **relative to its normal position**.

The element **still keeps its original space** in the layout.

### Example

```html
<div class="box">Box</div>
```

```css
.box {
  position: relative;
  top: 20px;
  left: 30px;
  background-color: lightblue;
}
```



---

## Position: Absolute

### What is Absolute Position?

`position: absolute` moves an element **relative to its nearest positioned parent**.

The element is **removed from the normal document flow**.

### Example

```html
<div class="container">
  <div class="box">Box</div>
</div>
```

```css
.container {
  position: relative;
  height: 200px;
  border: 1px solid black;
}

.box {
  position: absolute;
  top: 20px;
  right: 20px;
  background-color: lightgreen;
}
```

---




## Common CSS Structural Classes

### What are Structural Classes?

Structural classes are used to **organize the layout of a webpage**.

They help divide the page into sections like header, content, and footer.

### Common Structural Classes

* `.container`
* `.header`
* `.navbar`
* `.content`
* `.sidebar`
* `.footer`

### Example

```html
<div class="container">
  <div class="header">Header</div>
  <div class="content">Main Content</div>
  <div class="footer">Footer</div>
</div>
```

```css
.container {
  width: 80%;
  margin: auto;
}

.header {
  background: lightblue;
}

.content {
  background: lightgray;
}

.footer {
  background: lightgreen;
}
```

### Explanation

* `.container` → main wrapper of page
* `.header` → top section of page
* `.content` → main content area
* `.footer` → bottom section

---

# Common CSS Styling Classes

### What are Styling Classes?

Styling classes are used to **change the appearance of elements**.

They control things like **color, size, spacing, and alignment**.

### Common Styling Classes

* `.text-center`
* `.text-bold`
* `.bg-color`
* `.margin`
* `.padding`





---

# CSS Specificity

### What is CSS Specificity?

CSS Specificity decides **which CSS rule is applied** when multiple rules target the same element.

The rule with **higher priority (specificity)** will be applied.

### Specificity Order (Low to High)

1. Element selector
2. Class selector
3. ID selector
4. Inline style





---



# CSS Layout & Responsiveness

## CSS Responsive Media Queries

### What are Media Queries?

Media queries are used to **make a website responsive** for different screen sizes like **mobile, tablet, and desktop**.

### Syntax

```css
@media (condition) {
  /* CSS rules */
}
```

### Example

```css
.container {
  background: lightblue;
}

@media (max-width: 600px) {
  .container {
    background: lightgreen;
  }
}
```



### Common Breakpoints

| Device  | Screen Size    |
| ------- | -------------- |
| Mobile  | below 480px    |
| Tablet  | 480px – 1024px |
| Desktop | above 1024px   |

### Example

```css
/* Mobile */
@media (max-width: 480px) {
  body {
    font-size: 14px;
  }
}

/* Tablet */
@media (min-width: 481px) and (max-width: 1024px) {
  body {
    font-size: 16px;
  }
}

/* Desktop */
@media (min-width: 1025px) {
  body {
    font-size: 18px;
  }
}
```

---

# 2. Flexbox

### What is Flexbox?

Flexbox is used to **align and arrange items in a row or column easily**.

### Basic Example

```html
<div class="container">
  <div>Item 1</div>
  <div>Item 2</div>
  <div>Item 3</div>
</div>
```

```css
.container {
  display: flex;
}
```

### Important Flexbox Properties

| Property        | Use                  |
| --------------- | -------------------- |
| display: flex   | Enables flexbox      |
| flex-direction  | Row or column layout |
| justify-content | Horizontal alignment |
| align-items     | Vertical alignment   |

### Example

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```



---

# CSS Grid

### What is Grid?

CSS Grid is used to **create two-dimensional layouts (rows and columns)**.

### Example

```html
<div class="grid">
  <div>1</div>
  <div>2</div>
  <div>3</div>
</div>
```

```css
.grid {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
}
```
---

# Common HTML Header Meta Tags

## What are Meta Tags?

Meta tags are placed inside the **`<head>` section** of an HTML document.
They provide **information about the webpage** to browsers and search engines.

---

## 1. Charset Meta Tag

### Purpose

Defines the **character encoding** for the webpage.

### Example

```html
<meta charset="UTF-8">
```

### Explanation

* `UTF-8` supports most characters and languages.

---

## 2. Viewport Meta Tag

### Purpose

Makes the webpage **responsive on mobile devices**.

### Example

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

### Explanation

* `width=device-width` → sets page width to device width
* `initial-scale=1.0` → sets initial zoom level

---

## 3. Description Meta Tag

### Purpose

Provides a **short description of the webpage** for search engines.

### Example

```html
<meta name="description" content="This is a simple website about HTML and CSS.">
```
---
# Any other topic I think is important

## Setting Width and Height for Inline Elements

### Problem

Inline elements normally **do not accept width and height**.

Examples of inline elements:

* `<span>`
* `<a>`
* `<strong>`
* `<em>`

If you apply width or height, it **will not work**.

### Example

```html
<span class="box">Text</span>
```

```css
.box {
  width: 200px;
  height: 100px;
  background: lightblue;
}
```

Result:
Width and height **will not apply**.

---

## Solution

To apply width and height to inline elements, change the **display property**.

### 1. Using `inline-block`

`inline-block` keeps the element **inline** but allows **width and height**.

```css
.box {
  display: inline-block;
  width: 200px;
  height: 100px;
  background: lightblue;
}
```

Now width and height **will work**.

---

### 2. Using `block`

You can also convert it into a **block element**.

```css
.box {
  display: block;
  width: 200px;
  height: 100px;
}
```

This makes the element behave like a **block element**.




---


# References

1. **MDN Web Docs**
   https://developer.mozilla.org  
   Official documentation for HTML and CSS concepts.

2. **W3Schools**
   https://www.w3schools.com  
   Beginner-friendly explanations and examples for HTML, CSS, and web development.

---



