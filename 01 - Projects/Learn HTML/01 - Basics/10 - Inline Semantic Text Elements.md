```html
<!-- abbr — abbreviation or acronym -->
<p>I write notes in <abbr title="Markdown">MD</abbr> format.</p>
<p><abbr title="HyperText Markup Language">HTML</abbr> is the language of the web.</p>

<!-- cite — title of a creative work -->
<p>I just finished reading <cite>The Pragmatic Programmer</cite>.</p>
<blockquote>
  <p>Don't panic.</p>
  <footer>— <cite>The Hitchhiker's Guide to the Galaxy</cite></footer>
</blockquote>

<!-- q — short inline quotation (browser adds quotation marks) -->
<p>He said <q>the meeting starts at nine</q> and left.</p>
<p lang="fr"><q lang="en">Hello</q> means <q>bonjour</q>.</p>

<!-- kbd — keyboard input -->
<p>Press <kbd>Ctrl</kbd> + <kbd>S</kbd> to save.</p>
<p>To open the terminal, press <kbd>Ctrl</kbd> + <kbd>Alt</kbd> + <kbd>T</kbd>.</p>

<!-- samp — sample output from a program -->
<p>The command returned: <samp>Error: file not found</samp></p>
<pre><samp>
$ go run main.go
Hello, World!
</samp></pre>

<!-- var — a variable in math or programming -->
<p>The equation is <var>E</var> = <var>m</var><var>c</var><sup>2</sup>.</p>
<p>The function takes argument <var>n</var> and returns <var>n</var> × 2.</p>

<!-- dfn — defines a term (the defining instance) -->
<p>
  <dfn id="html-def">HTML</dfn> (HyperText Markup Language) is the standard
  language for creating web pages.
</p>
<p>Later I can <a href="#html-def">reference that definition</a>.</p>

<!-- small — side comment, fine print, legal text -->
<p>Buy now for $29.99 <small>(excluding tax)</small></p>
<footer><small>&copy; 2025 My Company. All rights reserved.</small></footer>

<!-- s — strikethrough for no-longer-accurate content -->
<p>Was: <s>$59.99</s> — Now: $29.99</p>
<p>The event is <s>on Friday</s> on Saturday.</p>

<!-- mark — highlighted / relevant text -->
<p>Search results for "html":
  Learning <mark>HTML</mark> is the first step to web development.
</p>

<!-- time — machine-readable date/time -->
<p>Published on <time datetime="2025-03-15">March 15, 2025</time>.</p>
<p>The meeting is at <time datetime="14:30">2:30 PM</time>.</p>
<p>It happened <time datetime="2025-03-15T14:30:00+05:00">last Tuesday afternoon</time>.</p>

<!-- sub and sup — subscript and superscript -->
<p>Water is H<sub>2</sub>O.</p>
<p>Einstein's formula: E = mc<sup>2</sup></p>
<p>See footnote<sup><a href="#fn1">[1]</a></sup> for details.</p>

<!-- wbr — word break opportunity -->
<p>This is a superlongwordthatmightoverflow<wbr />butcanbreakhere if needed.</p>
<p>https://www.example.com/very/long/<wbr />path/that/can/<wbr />break/here</p>

<!-- bdi — bidirectional isolation -->
<p>User <bdi>مرحبا</bdi> posted a comment.</p>

<!-- bdo — bidirectional override -->
<p><bdo dir="rtl">This text is forced right-to-left</bdo></p>
```

# Explanation

Beyond `<strong>` and `<em>`, HTML has a collection of inline semantic elements for very specific types of content — abbreviations, citations, keyboard shortcuts, program output, variable names, definitions, and more. Using the right element communicates exact meaning to screen readers, search engines, and browser features.

## Breakdown

- **`<abbr title="...">`**  
  Marks an abbreviation or acronym. The `title` attribute contains the full expansion. Browsers typically render a dotted underline. Screen readers may announce the expansion. Use it on the **first occurrence** of an abbreviation on the page.

- **`<cite>`**  
  The title of a referenced creative work — book, film, song, painting, article, game. Italic by default. Not for the author's name — only the work's title.

- **`<q>`**  
  A short inline quotation. Browsers automatically add locale-appropriate quotation marks around the content. Use `<blockquote>` for longer, block-level quotations. The `cite` attribute holds a URL to the source.

- **`<kbd>`**  
  Keyboard input — keys the user should press. Monospace font by default. Style with CSS (border, rounded corners) to resemble physical keycaps. Nest multiple `<kbd>` inside an outer `<kbd>` for key combinations.

- **`<samp>`**  
  Sample output from a computer program — what appears in the terminal or a dialog box. Monospace font by default. Distinguishes program output from surrounding prose.

- **`<var>`**  
  A variable — in a mathematical expression or in program code. Italic by default. Use inside prose when referring to a variable by name ("where *n* is the input").

- **`<dfn>`**  
  The defining instance of a term — the place in the text where a term is introduced and defined. Can be linked with `id` so other parts of the document can reference it with `<a href="#id">`.

- **`<small>`**  
  Fine print, side comments, and legal text — content that is secondary to the main content. Not "small text for styling" — use CSS `font-size` for that. Appropriate for copyright notices, disclaimers, and attribution.

- **`<s>`**  
  Content that is no longer accurate or relevant but should remain visible (strikethrough). Different from `<del>` — `<del>` marks edits to a document; `<s>` marks content that is outdated (like a crossed-out price).

- **`<mark>`**  
  Text highlighted as relevant to the user's current context — search result matches, referenced text, or a passage currently being discussed. Yellow background by default.

- **`<time datetime="...">`**  
  A specific point in time or a duration. Human-readable display text; machine-readable value in the `datetime` attribute (ISO 8601 format). Used by search engines, calendars, and browser features to parse dates.

- **`<sub>` / `<sup>`**  
  Subscript (below the line — chemical formulas, footnote numbers) and superscript (above the line — exponents, ordinal suffixes like 1st). Both reduce font size and shift vertical position.

- **`<wbr>` (Word Break Opportunity)**  
  Suggests a point where the browser *may* break a long word or URL across lines if needed. Unlike a hyphen, it's invisible — the break only happens if the line would otherwise overflow.

- **`<bdi>` (Bidirectional Isolation)**  
  Isolates a span of text so its direction is determined by its own content, not the surrounding text. Critical when displaying user-generated content (names, usernames) that may be in a different script direction.

- **`<bdo dir="...">` (Bidirectional Override)**  
  Forces the text rendering direction regardless of the content's natural direction. `dir="rtl"` forces right-to-left; `dir="ltr"` forces left-to-right.

## Key Points / Notes

- `<cite>` is for **work titles only** — not for attributing quotes to a person. `<blockquote cite="url">` is for attribution URLs, not the author's name.
- `<s>` vs `<del>`: use `<s>` for "this is no longer true" (sale prices, cancelled items). Use `<del>` for document edits showing what was removed (often paired with `<ins>`).
- `<mark>` vs `<strong>`: `<mark>` highlights for relevance in a specific context (search). `<strong>` marks importance in the content itself.
- `<kbd>` pairs well with CSS: `kbd { border: 1px solid #ccc; border-radius: 3px; padding: 2px 6px; font-family: monospace; }` produces convincing keyboard key styling.
- `<time>` without a `datetime` attribute is valid if the text content is itself a machine-parseable date — but always include `datetime` for clarity and reliability.
