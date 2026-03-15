```html
<!-- id — unique identifier -->
<div id="hero-section">...</div>
<a href="#hero-section">Jump to hero</a>

<!-- class — one or more style/behaviour hooks -->
<p class="text-muted small">Muted small text.</p>
<button class="btn btn--primary btn--lg">Save</button>

<!-- style — inline CSS (avoid in production) -->
<p style="color: #00ADD8; font-weight: 600;">Inline styled text.</p>

<!-- title — tooltip on hover -->
<abbr title="HyperText Markup Language">HTML</abbr>
<button title="Save your changes (Ctrl+S)">Save</button>

<!-- hidden — removes from display and accessibility tree -->
<div hidden>This is not rendered at all.</div>
<p hidden id="error-msg">An error occurred.</p>

<!-- tabindex — keyboard focus control -->
<div role="button" tabindex="0">Focusable custom element</div>
<button tabindex="-1">Not in tab order</button>

<!-- contenteditable — makes any element editable -->
<p contenteditable="true">Click here to edit this text directly.</p>
<div contenteditable="true" spellcheck="true">Editable with spellcheck.</div>

<!-- spellcheck -->
<textarea spellcheck="true">Browser checks spelling here.</textarea>
<input type="text" spellcheck="false" />

<!-- draggable -->
<div draggable="true" ondragstart="handleDrag(event)">Drag me!</div>

<!-- translate — hint to translation tools -->
<p translate="yes">This text should be translated.</p>
<code translate="no">console.log("Don't translate this")</code>

<!-- dir — text direction -->
<p dir="ltr">Left to right (default for English)</p>
<p dir="rtl">Right to left — for Arabic, Hebrew, Urdu</p>
<p dir="auto">Let the browser detect direction automatically</p>

<!-- lang — language of the element's content -->
<p>The French word is <span lang="fr">bonjour</span>.</p>

<!-- data-* — custom data attributes -->
<button data-user-id="42" data-action="delete">Delete</button>

<!-- accesskey — keyboard shortcut (rarely used) -->
<button accesskey="s">Save (Alt+S)</button>

<!-- autocapitalize — mobile keyboard capitalisation -->
<input type="text" autocapitalize="words" placeholder="Full name" />
<input type="text" autocapitalize="none"  placeholder="Username" />
```

# Explanation

Global attributes can be applied to **any HTML element**, regardless of type. They provide universal functionality — identity (`id`, `class`), visibility (`hidden`), accessibility (`tabindex`, `lang`), editing (`contenteditable`, `spellcheck`), and custom data (`data-*`).

## Breakdown

- **`id`**  
  A unique identifier for the element on the page. Used by CSS (`#id`), JavaScript (`getElementById`, `querySelector`), and fragment links (`href="#id"`). Must be unique — no two elements should share an `id`.

- **`class`**  
  One or more space-separated class names. The primary hook for CSS styling and JavaScript selection. Multiple elements can share a class; one element can carry many classes.

- **`style`**  
  Inline CSS applied directly to the element. Highest specificity of all CSS — overrides external stylesheets. Avoid for anything beyond truly one-off cases; use a class and external CSS instead.

- **`title`**  
  A tooltip string shown on hover (desktop only). Also used by screen readers in some contexts. Don't rely on it as the only way to convey important information — invisible on touch devices.

- **`hidden`**  
  A boolean attribute equivalent to `display: none`. Removes the element from rendering and from the accessibility tree. Semantically means "not currently relevant" — the element may become visible later. Not the same as `visibility: hidden` (which hides visually but keeps space).

- **`tabindex`**  
  Controls keyboard focus:  
  - `0` — adds the element to the natural tab order at its DOM position.  
  - `-1` — focusable via `.focus()` in JavaScript only, removed from Tab key sequence.  
  - Positive integers — explicit order (avoid: creates unpredictable navigation).

- **`contenteditable`**  
  Makes the element's content directly editable in the browser — like a rich text area. `"true"` enables editing, `"false"` explicitly disables it (useful for nested elements inside an editable parent). Used as the foundation of browser-based text editors.

- **`spellcheck`**  
  `"true"` enables the browser's built-in spell checking on the element. `"false"` disables it. Defaults vary by element and browser. Useful to disable on `<code>` and username fields.

- **`draggable`**  
  `"true"` makes the element draggable via the HTML Drag and Drop API. Fires `dragstart`, `drag`, and `dragend` events. `"false"` explicitly prevents dragging (e.g., on images, which are draggable by default).

- **`translate`**  
  A hint to browser translation features and translation services. `"yes"` (default) — translate this content. `"no"` — do not translate (use on brand names, code, proper nouns).

- **`dir`**  
  Text directionality. `"ltr"` (left-to-right), `"rtl"` (right-to-left, for Arabic, Hebrew, Urdu), `"auto"` (browser detects from the content). Set `dir="rtl"` on `<html>` for fully RTL pages.

- **`lang`**  
  Declares the language of the element's content as a BCP 47 tag (`"en"`, `"ur"`, `"fr"`). Screen readers switch pronunciation rules. Search engines use it for language-specific indexing. Set on `<html>` for the whole page; on individual elements for inline language switches.

- **`accesskey`**  
  Defines a keyboard shortcut (usually Alt+key on Windows, Ctrl+Alt+key on Mac). Rarely used in practice — conflicts with browser and OS shortcuts are common. Mention in a `title` tooltip if used.

- **`autocapitalize`**  
  Controls auto-capitalisation on mobile virtual keyboards. `"none"` — no capitalisation (for usernames, email). `"words"` — capitalize each word (for names). `"sentences"` (default for most inputs) — capitalize sentence starts. `"characters"` — capitalize all.

## Key Points / Notes

- `id` must be unique per page. Duplicate IDs cause silent failures in JavaScript (`getElementById` returns only the first) and invalid HTML.
- `hidden` is preferable to `style="display:none"` for toggling visibility because it is semantic (conveys intent) and can be toggled with a single `el.hidden = true/false` in JavaScript.
- `contenteditable` does not save content automatically — use JavaScript to capture the content and send it to a server.
- `dir="rtl"` affects not just text alignment but also layout — margins, padding, floats, and Flexbox/Grid row direction are all mirrored. Use the CSS `logical properties` (`margin-inline-start` instead of `margin-left`) for RTL-compatible layouts.
- `data-*` attributes are also global — any `data-anything` attribute is valid on any element. See the **Data Attributes** note in the Advanced section for full coverage.
