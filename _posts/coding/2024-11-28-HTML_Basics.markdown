---
layout: post
title:  "HTML Basics for Beginners"
description: "A beginner-friendly guide to understanding and using HTML to create your first webpage."
date:   2024-11-28 9:55:57 -0600
categories: coding web HTML
---
Welcome to the world of HTML! This guide is perfect for anyone starting their journey into web development. Learn how to create the building blocks of webpages step by step.

## What is HTML?

HTML stands for **HyperText Markup Language** and is used to define the content and structure of a website.

- **Hypertext**: Links that connect different parts of a website or other resources.
- **Markup**: Tags that format and organize content.
- **Language**: A system of rules for writing code.

Early websites were built with HTML alone. Over time, **CSS** and **JavaScript** were added for styling and interactive functionality.

## Heading Elements

Heading elements (`<h1>` to `<h6>`) are used to create headings, with `<h1>` being the largest and `<h6>` the smallest.

### Best Practices:
- **Use only one `<h1>` per page** for better SEO and accessibility.
- **Avoid skipping levels** (e.g., don’t jump from `<h1>` to `<h4>`).

Example of an `<h1>` element:
```html
<h1>Hello World</h1>
```
![html element image]({{ "/assets/html_element.png" | relative_url }})

## Paragraph Elements
Paragraphs are used to separate text into readable blocks. They follow the same structure as heading elements.
```html
<p>My Paragraph</p>
```

## Void Elements

So far we covered Non-Void elements which have two tags and content. However, Void elements don't have content or closing tags.

### Horizontal Rule (`<hr>`)

Adds a horizontal line to separate sections:
```html
<p>Paragraph 1</p>
<hr>
<p>Paragraph 2</p>
```


### Line Break (`<br>`)

Creates a new line within a paragraph:
```html
<p>Paragraph 1</p>
<br>
<p>Paragraph 2</p>
```
> 💡 **Tip:** Use `<p>`for new paragraphs rather than relying on `<br>` for layout.

## List Elements

HTML supports two types of lists:

1. **Unordered Lists** (bulleted):

```html
<ul>
    <li>Notebook</li>
    <li>Keyboard</li>
    <li>Mouse</li>
    <li>Charger</li>
</ul>
```
2. **Ordered Lists** (numbered):

```html
<ol>
    <li>Boil Water</li>
    <li>Add Salt</li>
    <li>Add Pasta</li>
    <li>Cook Pasta</li>
</ol>
```

![list element image]({{ "/assets/list_element.png" | relative_url }})

### Nested Lists

Lists can be nested inside one another for more complex structures. Ensure proper indentation for readability.

```html
<ul>
    <li>A</li>
        <ol>
            <li>A1</li>
            <li>A2</li>
        </ol>
    <li>B</li>
    <li>C</li>
</ul>
```

## Anchor Elements

Anchor elements (`<a>`) are hyperlinks that link to other pages or resources. The link address is defined in the attribute section. 

```html
<a href="https://www.google.com">Thats a Goole Link</a>
```
There are a bunch of attributes that you can add to HTML elements. They are added in he opening tag like this:

![anchor element image]({{ "/assets/anchor_element.png" | relative_url }})

## Image Elements

Images are added using the `<img>` element, a void element.

### Required Attributes:

- `src` **Source Attribute** The image source URL.
- `alt` **Alt Attribute** Alternative text describing the image for accessibility.

```html
<img src="https://picsum.photos/200" alt="Image Description"/>
```

> 💡 **Tip:** Always include `alt`text for better accessibility and SEO. 