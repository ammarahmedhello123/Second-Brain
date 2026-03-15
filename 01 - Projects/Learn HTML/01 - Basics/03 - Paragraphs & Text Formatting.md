```html
<p>This is a paragraph of text.</p>

<p>
  Make text <strong>bold and important</strong> or just <b>visually bold</b>.
  Add <em>stressed emphasis</em> or just <i>italic styling</i>.
  <mark>Highlight relevant text.</mark>
  Show <del>removed text</del> and <ins>inserted text</ins>.
  Subscript: H<sub>2</sub>O — Superscript: x<sup>2</sup>
</p>

<p>Inline code: <code>console.log("hello")</code></p>

<pre><code>
function greet() {
  return "Hello!";
}
</code></pre>

<blockquote cite="https://source.com">
  A meaningful quote pulled from another source.
</blockquote>

<p>Line one.<br />Line two forced below.</p>

<hr />
```

# Explanation

These tags handle the core written content of a page. The key principle is that HTML tags should convey **meaning**, not just appearance. `<strong>` means "this is important" — it just happens to look bold by default.

## Breakdown

- **`<p>`**  
  A paragraph. Block-level — starts on a new line and has default top and bottom margin. The most common container for body text.

- **`<strong>`**  
  Marks text as having strong importance. Browsers render it bold; screen readers may give it added stress when reading aloud. Use when the content is genuinely critical.

- **`<b>`**  
  Visually bold with no semantic importance — for stylistic use like keywords in a summary. Conveys no extra meaning to assistive technology.

- **`<em>`**  
  Stressed emphasis — the kind that changes a sentence's meaning ("I *never* said that"). Screen readers may alter intonation here.

- **`<i>`**  
  Italic styling with no semantic emphasis — for technical terms, foreign phrases, or stylistic choice. No implied importance.

- **`<mark>`**  
  Highlights text as relevant to the user's current context (like a search match). Yellow background by default.

- **`<del>` and `<ins>`**  
  Represent text that was removed (`<del>`, renders as strikethrough) or added (`<ins>`, renders underlined). Useful for edits and changelogs.

- **`<sub>` and `<sup>`**  
  Subscript (H₂O) and superscript (x²). Essential for chemistry, math, and footnote references.

- **`<code>`**  
  Inline code or technical terms. Monospace font by default.

- **`<pre><code>`**  
  For multi-line code blocks. `<pre>` preserves all whitespace and line breaks exactly as written. `<code>` inside it marks it as code.

- **`<blockquote>`**  
  A block-level quotation from an external source. Indented by default. The `cite` attribute holds the source URL (not displayed, but semantic).

- **`<br />`**  
  A forced line break within flowing text. Use sparingly — never as a substitute for paragraph spacing.

- **`<hr />`**  
  A thematic break — semantically means "a shift in topic." Not just a decorative line.

## Key Points / Notes

- `<strong>` vs `<b>` and `<em>` vs `<i>`: the semantic pair is almost always the right choice. Use the stylistic pair only when meaning is genuinely absent.
- Never use `<br><br>` between paragraphs — use separate `<p>` tags, and control spacing with CSS `margin`.
- `<blockquote>` is for actual quotations, not for indenting content.
- Inline elements (`<strong>`, `<em>`, `<code>`) go inside block elements (`<p>`, `<li>`). Never put a `<p>` inside a `<p>`.
- For preformatted multi-line code, always use `<pre><code>` — never a lone `<code>` tag.
