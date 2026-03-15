```html
<!-- div: block-level generic container -->
<div class="card">
  <div class="card__header">
    <h2>Card Title</h2>
  </div>
  <div class="card__body">
    <p>Card content goes here.</p>
  </div>
  <div class="card__footer">
    <button>Read More</button>
  </div>
</div>

<!-- span: inline generic container -->
<p>
  Your total is <span class="price">$49.99</span> including tax.
</p>

<p>
  Status: <span class="badge badge--success">Active</span>
</p>

<!-- Combining for layout -->
<div class="grid">
  <div class="col">
    <p>Left: <span class="highlight">key term</span> in sentence.</p>
  </div>
  <div class="col">
    <p>Right column content.</p>
  </div>
</div>
```

# Explanation

`<div>` and `<span>` are the two **non-semantic** generic containers. They carry no inherent meaning — they are purely structural hooks for applying CSS and JavaScript when no semantic element accurately fits the content.

## Breakdown

- **`<div>` (Division)**  
  A **block-level** container. Takes up the full width available and forces a new line before and after it. Wraps groups of elements so they can be styled or scripted as a single unit.

- **`<span>`**  
  An **inline** container. Flows within surrounding text without breaking the line. Targets a word or phrase inside a paragraph for styling or scripting without affecting text flow.

- **`class` attribute**  
  The primary hook for CSS and JavaScript. Multiple elements can share a class. One element can have multiple classes (space-separated): `class="btn btn--primary large"`.

- **`id` attribute**  
  A unique identifier — only **one** element per page should have a given `id`. Used for fragment links (`href="#id"`), JavaScript targeting, and CSS (though high specificity makes IDs in CSS an anti-pattern to avoid).

- **When to use `<div>`**  
  When you need a block-level wrapper for layout and no semantic element (`<section>`, `<article>`, `<header>`, `<nav>`, etc.) accurately describes the role of the content.

- **When to use `<span>`**  
  When you need to style or target an inline portion of text and no semantic element (`<strong>`, `<em>`, `<code>`, `<mark>`, `<time>`) accurately describes the content's meaning.

## Key Points / Notes

- The rule: **always reach for a semantic element first**. Only fall back to `<div>` or `<span>` when nothing semantic fits.
- `<div>` is block-level; `<span>` is inline. A block element cannot be validly nested inside an inline element — no `<div>` inside a `<span>`.
- Layers of nested `<div>` with no semantic purpose is called "div soup." It makes code harder to read and maintain. Semantic elements and proper CSS layouts (Grid, Flexbox) fix this.
- Duplicate `id` values on a page break `document.getElementById()`, invalidate the HTML, and cause unpredictable CSS behaviour.
- A `<div>` or `<span>` with no `class`, `id`, or attribute attached is completely inert — just extra markup with no effect.
