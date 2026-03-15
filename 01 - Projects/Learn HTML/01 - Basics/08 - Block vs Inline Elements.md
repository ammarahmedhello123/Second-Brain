```html
<!-- Block-level elements — take full width, start on a new line -->
<div>I am a block element</div>
<p>I am also a block element</p>
<h2>So am I</h2>
<ul>
  <li>And me</li>
</ul>

<!-- Inline elements — flow within text, take only as much width as needed -->
<p>
  This is a sentence with <strong>bold</strong>, <em>italic</em>,
  a <a href="#">link</a>, and <code>inline code</code> — all inline.
</p>

<!-- You can't put a block element inside an inline element -->
<!-- ❌ Invalid -->
<!-- <span><div>Content</div></span> -->
<!-- <a href="#"><p>Paragraph inside link</p></a> -->

<!-- ✅ Valid — inline inside block -->
<p><strong>This is fine.</strong> Inline inside block.</p>

<!-- ✅ Valid HTML5 exception — <a> can wrap block content -->
<a href="/article">
  <div class="card">
    <h3>Card Title</h3>
    <p>Clicking anywhere on this card navigates.</p>
  </div>
</a>

<!-- Inline-block — inline flow but accepts width/height like a block -->
<span style="display: inline-block; width: 100px; height: 40px; background: steelblue;"></span>
<span style="display: inline-block; width: 100px; height: 40px; background: coral;"></span>

<!-- Common block elements -->
<div>div</div>
<p>p</p>
<h1>h1–h6</h1>
<ul><li>ul, ol, li</li></ul>
<table><tr><td>table</td></tr></table>
<header>header</header>
<main>main</main>
<section>section</section>
<article>article</article>
<aside>aside</aside>
<footer>footer</footer>
<nav>nav</nav>
<form>form</form>
<blockquote>blockquote</blockquote>
<pre>pre</pre>
<hr />
<figure>figure</figure>

<!-- Common inline elements -->
<p>
  <a href="#">a</a>
  <strong>strong</strong>
  <em>em</em>
  <span>span</span>
  <code>code</code>
  <img src="" alt="" />
  <button>button</button>
  <label>label</label>
  <input type="text" />
  <small>small</small>
  <mark>mark</mark>
  <abbr>abbr</abbr>
  <time>time</time>
</p>
```

# Explanation

Every HTML element has a default **display type** — either block or inline. This determines how the element flows in the document, how much space it occupies, and what elements it can legally contain. Understanding this is foundational to both layout and valid HTML.

## Breakdown

- **Block-level elements**  
  Start on a new line and stretch to fill the full available width of their parent container. Stack vertically, one after another. Accept `width`, `height`, `margin`, and `padding` on all four sides.  
  Common examples: `<div>`, `<p>`, `<h1>`–`<h6>`, `<ul>`, `<ol>`, `<li>`, `<table>`, `<form>`, `<section>`, `<article>`, `<header>`, `<footer>`, `<main>`, `<nav>`, `<aside>`, `<blockquote>`, `<pre>`, `<figure>`, `<hr>`.

- **Inline elements**  
  Flow within the surrounding text — they don't start a new line. Only take up as much width as their content. Top/bottom `margin` and `padding` are ignored (or have limited effect). Cannot contain block-level elements.  
  Common examples: `<a>`, `<strong>`, `<em>`, `<span>`, `<code>`, `<img>`, `<button>`, `<input>`, `<label>`, `<small>`, `<mark>`, `<abbr>`, `<time>`, `<cite>`, `<kbd>`.

- **Nesting rules**  
  Block elements can contain both block and inline elements. Inline elements can only contain other inline elements (and text). Breaking this rule produces invalid HTML that browsers may silently "fix" in unpredictable ways.

- **The `<a>` exception**  
  In HTML5, `<a>` is a special "transparent" element — it can wrap block-level content (like a card `<div>`) to make the entire area a clickable link. The `<a>` itself is still inline, but HTML5 permits this pattern.

- **`display: inline-block`**  
  A CSS display value that combines both — the element flows inline (sits within text) but accepts block properties like `width`, `height`, and vertical `margin`/`padding`. Used for navigation items, tag chips, and avatar images.

- **`display` can always be overridden with CSS**  
  A `<div>` can be made inline with `display: inline`. A `<span>` can be made block with `display: block`. The HTML element's default display type is a CSS default — CSS always wins.

## Key Points / Notes

- Default display type is a CSS property (`display: block` or `display: inline`), not a fixed property of the element — CSS can change it freely.
- The most common mistake: putting a `<p>` inside a `<span>`, or a `<div>` inside a `<p>`. Browsers "fix" invalid nesting silently, producing a DOM that looks nothing like the source HTML.
- `<p>` is special — it cannot contain block-level children at all. The parser closes the `<p>` automatically when it encounters a block element inside it.
- `<img>` is technically inline but behaves oddly (it has a natural width and height). Setting `display: block` on images is a common CSS reset to eliminate the small gap that appears below inline images.
- Modern CSS layout (`Flexbox`, `Grid`) overrides block/inline entirely — all flex/grid children become "block-ified" regardless of their default display type.
