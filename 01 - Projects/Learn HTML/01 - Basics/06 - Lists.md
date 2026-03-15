```html
<!-- Unordered list (order doesn't matter) -->
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<!-- Ordered list (sequence matters) -->
<ol>
  <li>Boil water</li>
  <li>Add pasta</li>
  <li>Cook for 10 minutes</li>
  <li>Drain and serve</li>
</ol>

<!-- Ordered list — custom start number and letter type -->
<ol start="5" type="A">
  <li>Item E</li>
  <li>Item F</li>
</ol>

<!-- Nested list -->
<ul>
  <li>Frontend
    <ul>
      <li>HTML</li>
      <li>CSS</li>
      <li>JavaScript</li>
    </ul>
  </li>
  <li>Backend
    <ul>
      <li>Go</li>
      <li>Node.js</li>
    </ul>
  </li>
</ul>

<!-- Description list (term + definition pairs) -->
<dl>
  <dt>HTML</dt>
  <dd>HyperText Markup Language — the structure of the web.</dd>

  <dt>CSS</dt>
  <dd>Cascading Style Sheets — the visual presentation of the web.</dd>

  <dt>JavaScript</dt>
  <dd>The programming language of the web — adds interactivity.</dd>
</dl>
```

# Explanation

HTML has three types of lists: **unordered** for items where order doesn't matter, **ordered** for sequences and rankings, and **description lists** for term-definition pairs. Each has its own semantics that convey the relationship between items.

## Breakdown

- **`<ul>` (Unordered List)**  
  A list where the order of items is not significant. Displayed with bullet points by default. The visual style is fully controlled by CSS.

- **`<ol>` (Ordered List)**  
  A list where order *matters* — steps, rankings, or any sequence. Items are automatically numbered starting from 1.

- **`<li>` (List Item)**  
  A single item inside a `<ul>` or `<ol>`. Must be a direct child of the list element. Can contain any HTML — text, links, images, or nested lists.

- **`start` attribute**  
  On `<ol>` — sets the starting counter number. Useful when a list is split across a page and needs to continue from a previous number.

- **`type` attribute**  
  On `<ol>` — changes the counter style: `"1"` (numbers, default), `"A"` (uppercase letters), `"a"` (lowercase), `"I"` (uppercase Roman), `"i"` (lowercase Roman). Prefer CSS `list-style-type` for presentational control.

- **Nested list**  
  A list inside a list. The nested `<ul>` or `<ol>` goes *inside* an `<li>`, not directly inside the parent list. Used for navigation menus, outlines, and hierarchical data.

- **`<dl>` (Description List)**  
  A list of term-description pairs. Semantically perfect for glossaries, FAQs, metadata panels, and key-value displays.

- **`<dt>` (Description Term)**  
  The term being defined. Bold by default.

- **`<dd>` (Description Details)**  
  The definition or explanation. Indented by default.

## Key Points / Notes

- Only `<li>` elements should be direct children of `<ul>` and `<ol>`. Putting `<p>` or `<div>` directly inside is invalid HTML.
- Use CSS `list-style: none` to remove bullets or numbers — the semantics remain while the visual is customized. Navigation menus are commonly built this way.
- `<dl>` supports multiple `<dt>` per `<dd>` and multiple `<dd>` per `<dt>` — useful for complex glossary structures.
- Don't use lists purely for indentation or visual grouping. Use them when the content is genuinely a list of related items.
- The `reversed` attribute on `<ol>` counts down instead of up — useful for a Top 10 countdown format.
