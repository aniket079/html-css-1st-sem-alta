# UNIT II: VARIOUS TAGS IN HTML — Detailed Student Notes

---

## 📋 Syllabus Overview & Topic Mapping
According to the syllabus image uploaded, **Unit II / Module 2** covers the following core HTML topics:
1. **HTML Elements**
2. **HTML Attributes**
3. **Headings**
4. **Paragraphs**
5. **Styles**
6. **HTML Images**

---

## 1. HTML Elements

### 1.1 What is an HTML Element?
An **HTML Element** is the fundamental building block of an HTML document. It consists of a **start tag (opening tag)**, **content**, and an **end tag (closing tag)**.

```html
<tagname>Content goes here...</tagname>
```

* **Opening Tag (`<p>`):** Tells the browser where the element begins.
* **Content (`Hello World`):** The visible text, media, or nested elements inside.
* **Closing Tag (`</p>`):** Tells the browser where the element ends (marked with a forward slash `/`).

#### Example of Standard HTML Elements:
```html
<h1>Main Page Heading</h1>
<p>This is a text paragraph element.</p>
```

---

### 1.2 Types of HTML Elements

#### A. Container Elements
Elements that contain text or other elements between an opening tag and a closing tag.
* Examples: `<h1>...</h1>`, `<p>...</p>`, `<div>...</div>`, `<span>...</span>`.

#### B. Void (Empty) Elements
Elements that do **not** have content or a closing tag. They are self-contained.
* Examples:
  * `<br>` — Inserts a single line break.
  * `<hr>` — Inserts a horizontal thematic rule/line.
  * `<img>` — Embeds an image asset.

---

### 1.3 Block-Level vs. Inline Elements

| Feature | Block-Level Elements | Inline Elements |
| :--- | :--- | :--- |
| **Line Behavior** | Always starts on a **new line**. | Renders **inline** with surrounding text. |
| **Width** | Takes up the **full available width** (100%). | Takes up only as much width as its content needs. |
| **Examples** | `<div>`, `<h1>`-`<h6>`, `<p>`, `<table>` | `<span>`, `<a>`, `<img>`, `<strong>`, `<em>` |

---

## 2. HTML Attributes

### 2.1 What is an HTML Attribute?
**HTML Attributes** provide additional information or configurations for HTML elements. They are **always specified in the opening tag** and typically appear as `name="value"` pairs.

```html
<element attribute_name="attribute_value">Content</element>
```

---

### 2.2 Essential Global Attributes
Global attributes can be used on almost any HTML element:

* **`id`**: Specifies a unique identifier for an element (must be unique across the whole page).
  ```html
  <h1 id="main-header">Welcome to HTML Class</h1>
  ```
* **`class`**: Assigns one or more class names to an element (used for grouping and CSS styling).
  ```html
  <p class="highlight-text warning">Pay attention to this rule.</p>
  ```
* **`title`**: Adds extra information displayed as a tooltip when hovering over the element.
  ```html
  <p title="Tooltip text appears on hover">Hover your mouse over me!</p>
  ```
* **`lang`**: Specifies the language of the element's content.
  ```html
  <html lang="en">
  ```
* **`style`**: Applies inline CSS styling directly to the element.
  ```html
  <p style="color: blue;">Blue paragraph text.</p>
  ```

---

## 3. Headings (`<h1>` to `<h6>`)

### 3.1 Heading Hierarchy
HTML offers six levels of document headings, ranging from `<h1>` (most important / largest) down to `<h6>` (least important / smallest).

```html
<h1>Heading Level 1 (Main Title)</h1>
<h2>Heading Level 2 (Major Section)</h2>
<h3>Heading Level 3 (Sub-section)</h3>
<h4>Heading Level 4</h4>
<h5>Heading Level 5</h5>
<h6>Heading Level 6 (Smallest)</h6>
```

### 3.2 Best Practices for Headings
1. **Semantic Hierarchy:** Use headings to structure document content logically, not just to make text big or bold.
2. **Single `<h1>` Rule:** Maintain only **one `<h1>` per web page** representing the main title of the page.
3. **Sequential Order:** Never skip heading levels (e.g., do not jump directly from `<h1>` to `<h3>`).

---

## 4. Paragraphs & Formatting Lines (`<p>`, `<br>`, `<hr>`)

### 4.1 The Paragraph Element (`<p>`)
The `<p>` element defines a paragraph of text. Browsers automatically add vertical white space (margin) before and after every paragraph.

```html
<p>HTML stands for HyperText Markup Language. It is the standard language for creating web pages.</p>
<p>Browsers automatically insert spacing between separate paragraph elements.</p>
```

---

### 4.2 Line Break Element (`<br>`)
The `<br>` tag forces a line break within the same paragraph without creating extra paragraph spacing.

```html
<p>
  Student Name: Aniket<br>
  Course: Web Development<br>
  Semester: One
</p>
```

---

### 4.3 Horizontal Rule Element (`<hr>`)
The `<hr>` tag inserts a horizontal rule across the page, visually separating topics or sections.

```html
<h2>Section 1: Basics</h2>
<p>Introductory text here...</p>
<hr>
<h2>Section 2: Advanced Topics</h2>
<p>Next section text here...</p>
```

---

## 5. Styles & Text Formatting

### 5.1 The `style` Attribute (Inline Styles)
The `style` attribute allows styling individual HTML elements directly using CSS property-value pairs: `style="property: value;"`.

```html
<!-- Text Color -->
<p style="color: red;">This text is red.</p>

<!-- Background Color -->
<body style="background-color: #f0f4f8;">

<!-- Font Size & Font Family -->
<p style="font-family: Arial, sans-serif; font-size: 18px;">Custom typography.</p>

<!-- Text Alignment -->
<h2 style="text-align: center;">Centered Heading</h2>
```

---

### 5.2 Text Formatting Elements

| Tag | Purpose | Type |
| :--- | :--- | :--- |
| `<strong>` | Renders text **bold** with **high semantic importance** (screen readers emphasize it). | Semantic |
| `<b>` | Renders text **bold** for visual drawing without extra semantic importance. | Presentational |
| `<em>` | Renders text *italicized* with *semantic stress emphasis*. | Semantic |
| `<i>` | Renders text *italicized* for technical terms, idioms, or thoughts. | Presentational |
| `<u>` | Renders text <u>underlined</u>. | Presentational |
| `<mark>` | Highlights text with a <mark>yellow background fill</mark>. | Visual |
| `<small>` | Decreases text size to render fine print or disclaimers. | Visual |
| `<sub>` | Renders text as <sub>subscript</sub> (e.g., H<sub>2</sub>O). | Special |
| `<sup>` | Renders text as <sup>superscript</sup> (e.g., 10<sup>2</sup> = 100). | Special |

#### Formatting Code Example:
```html
<p>
  This is <strong>very important</strong> and <em>emphasized</em> text.<br>
  Chemical formula for water: H<sub>2</sub>O<br>
  Mathematical equation: E = mc<sup>2</sup><br>
  Important note: <mark>Exam starts at 9:00 AM</mark>.
</p>
```

---

## 6. HTML Images (`<img>`)

### 6.1 Syntax & Primary Attributes
The `<img>` element is a self-closing void tag used to embed raster or vector graphics into a webpage.

```html
<img src="image_url_or_path" alt="Descriptive text" width="300" height="200">
```

* **`src` (Source):** Specifies the relative or absolute path to the image file (Required).
* **`alt` (Alternative Text):** Provides a descriptive text replacement if the image fails to load or for screen readers used by visually impaired users (Required for accessibility).
* **`width` & `height`:** Defines the display dimensions in pixels.

---

### 6.2 Understanding Image File Paths

#### A. Same Directory:
If the image file is in the exact same folder as the HTML file:
```html
<img src="logo.png" alt="Company Logo">
```

#### B. Sub-directory:
If the image file is inside a child folder named `images`:
```html
<img src="images/photo.jpg" alt="Student Photo">
```

#### C. Parent Directory:
If the image file is located one level up in the parent folder:
```html
<img src="../banner.png" alt="Header Banner">
```

#### D. Absolute External URL:
Pointing directly to a file hosted on the internet:
```html
<img src="https://www.example.com/assets/logo.png" alt="External Logo">
```

---

### 6.3 Clickable Images (Image as a Link)
Nest the `<img>` tag inside an `<a>` (anchor) tag to turn an image into a clickable link:

```html
<a href="https://www.google.com" target="_blank">
  <img src="google_logo.png" alt="Google Homepage" width="150">
</a>
```

---

## 🧪 Unit II Practical Laboratory Assignment

### Task: Build a Personal Profile Webpage
Create an HTML file named `unit2_practice.html` that implements all the concepts covered in Unit II:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Unit 2 Practice - Personal Profile</title>
</head>
<body style="background-color: #fafafa; font-family: Arial, sans-serif; line-height: 1.6; padding: 20px;">

  <!-- Main Title -->
  <h1 style="color: #1a365d; text-align: center;">Student Profile: Alex Johnson</h1>
  <hr>

  <!-- About Section -->
  <h2>About Me</h2>
  <p>
    Hello! My name is <strong>Alex Johnson</strong>. I am currently enrolled in the <em>HTML & CSS Semester One</em> course.<br>
    My goal is to become a skilled <mark>Full-Stack Web Developer</mark>.
  </p>

  <!-- Profile Picture -->
  <h2>Profile Picture</h2>
  <img src="profile.jpg" alt="Alex Johnson Profile Picture" width="200" style="border-radius: 8px;">

  <!-- Favorite Quotes & Formatted Text -->
  <h2>Key Notes & Science Trivia</h2>
  <p>
    My favorite scientific formula is <strong>E = mc<sup>2</sup></strong>, and the chemical symbol for water is <strong>H<sub>2</sub>O</strong>.<br>
    <small>Note: All HTML assignments must be submitted before Friday.</small>
  </p>

</body>
</html>
```
