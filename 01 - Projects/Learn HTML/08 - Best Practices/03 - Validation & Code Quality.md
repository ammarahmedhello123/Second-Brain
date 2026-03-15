```html
<!-- ✅ CORRECT: Valid, well-formed HTML -->
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Unique Page Title</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>

  <header>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
      </ul>
    </nav>
  </header>

  <main id="main-content">
    <h1>Clear, Descriptive Heading</h1>
    <p>Well-structured, readable content.</p>

    <!-- Correct: label linked to input by matching for/id -->
    <label for="email">Email</label>
    <input type="email" id="email" name="email" required />

    <!-- Correct: button inside form has explicit type -->
    <button type="submit">Subscribe</button>
    <button type="button" onclick="clearForm()">Clear</button>
  </main>

  <footer>
    <p>&copy; 2025 My Site</p>
  </footer>

  <script src="app.js" defer></script>
</body>
</html>


<!-- ❌ COMMON MISTAKES TO AVOID -->

<!-- Missing alt on image -->
<!-- <img src="photo.jpg"> -->

<!-- Using <div> for a button (breaks keyboard access) -->
<!-- <div onclick="submit()">Submit</div> -->

<!-- Skipping heading levels -->
<!-- <h1>Title</h1><h4>Subtitle</h4> -->

<!-- Label not connected to input -->
<!-- <label>Email</label><input type="email"> -->

<!-- Nesting block elements inside inline elements -->
<!-- <span><div>Content</div></span> -->

<!-- Using tables for layout -->
<!-- <table><tr><td>Left</td><td>Right</td></tr></table> -->

<!-- Form method missing for sensitive data -->
<!-- <form action="/login"><input type="password" name="pw"></form> -->

<!-- Missing DOCTYPE -->
<!-- <html><head>...</head><body>...</body></html> -->
```

# Explanation

Valid HTML is consistent, predictable HTML. Browsers apply "quirks mode" to invalid HTML and may interpret it differently across vendors. Code quality in HTML means: correct nesting, proper semantics, no deprecated patterns, and consistent formatting.

## Breakdown

- **W3C Markup Validator**  
  The official tool for validating HTML: `validator.w3.org`. Paste a URL or upload a file. It flags actual errors (invalid nesting, missing required attributes) and warnings (deprecated elements, suspicious patterns). Run it on every new page.

- **Correct nesting**  
  HTML elements must be properly nested — inner tags closed before outer tags. `<p><strong>text</strong></p>` ✅ — `<p><strong>text</p></strong>` ❌. Block elements (`<div>`, `<p>`) cannot be nested inside inline elements (`<span>`, `<a>`).

- **All attributes quoted**  
  Always use quotes around attribute values: `id="header"`, not `id=header`. Unquoted values break with spaces, special characters, and some parsers.

- **Self-closing void elements**  
  Elements with no content (`<img>`, `<input>`, `<br>`, `<hr>`, `<meta>`, `<link>`) can be written with a trailing slash (`<img />`) or without (`<img>`). In HTML5, both are valid. Pick one style and be consistent.

- **Lowercase tags and attributes**  
  HTML is case-insensitive, but lowercase is the universal convention. `<HTML>` is valid but `<html>` is what every developer and linter expects.

- **Indentation**  
  Indent child elements consistently (2 or 4 spaces, never tabs mixed with spaces). Indentation makes nesting depth immediately visible, which prevents closing-tag errors.

- **Separation of concerns**  
  HTML = structure. CSS = presentation. JS = behaviour. Avoid `style=""` attributes and `onclick=""` inline handlers in production code. Mixing them makes code hard to maintain and impossible to reuse.

- **`<button type>` always explicit**  
  A `<button>` inside a form defaults to `type="submit"`. Always specify `type="button"` for non-submit buttons to prevent accidental form submissions — one of the most common subtle bugs in HTML forms.

- **No deprecated elements**  
  `<center>`, `<font>`, `<marquee>`, `<blink>`, `<frameset>` are obsolete. `<b>` and `<i>` are technically valid but prefer `<strong>` and `<em>` for semantic clarity.

## Key Points / Notes

- Invalid HTML doesn't always break visually — browsers are very forgiving. But it causes inconsistent rendering across browsers, breaks accessibility trees, and creates hard-to-debug CSS and JS issues.
- Use a linter like **HTMLHint** or **Prettier** in your editor to catch mistakes as you type, not after the fact.
- The **axe DevTools** browser extension checks HTML for accessibility violations in one click — more actionable than the W3C validator for day-to-day work.
- A consistent code style matters more than which style you pick. Whatever indentation, quoting, and self-closing convention you choose, apply it everywhere.
- Final checklist before publishing: ✅ Valid HTML, ✅ unique title and description, ✅ all images have alt text, ✅ all inputs have labels, ✅ heading hierarchy is correct, ✅ scripts have `defer`/`async`, ✅ no console errors.
