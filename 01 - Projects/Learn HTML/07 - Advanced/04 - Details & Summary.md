```html
<!-- Basic accordion / disclosure -->
<details>
  <summary>What is HTML?</summary>
  <p>
    HTML (HyperText Markup Language) is the standard markup language for creating
    web pages. It describes the structure of a web page using elements and tags.
  </p>
</details>

<!-- Open by default -->
<details open>
  <summary>Getting Started</summary>
  <p>Begin by creating a file named <code>index.html</code>...</p>
</details>

<!-- FAQ section using multiple details -->
<section>
  <h2>Frequently Asked Questions</h2>

  <details>
    <summary>Is HTML a programming language?</summary>
    <p>No — HTML is a markup language. It describes structure and content,
    but has no logic, conditionals, or loops. JavaScript is the programming language of the web.</p>
  </details>

  <details>
    <summary>Do I need to install anything to write HTML?</summary>
    <p>No. A plain text editor (even Notepad) and a browser are all you need.
    A proper code editor like VS Code makes things much easier though.</p>
  </details>

  <details>
    <summary>What is the difference between HTML and CSS?</summary>
    <p>HTML defines the <strong>structure and content</strong> of a page.
    CSS defines the <strong>visual presentation</strong> — colors, fonts, layout.</p>
  </details>
</section>

<!-- Accordion — only one open at a time (HTML 2024 name attribute) -->
<details name="faq">
  <summary>Question One</summary>
  <p>Answer one.</p>
</details>
<details name="faq">
  <summary>Question Two</summary>
  <p>Answer two.</p>
</details>
<details name="faq">
  <summary>Question Three</summary>
  <p>Answer three.</p>
</details>

<style>
  details {
    border: 1px solid #1e2229;
    border-radius: 8px;
    padding: 0;
    margin-bottom: 8px;
    overflow: hidden;
  }

  summary {
    padding: 14px 16px;
    cursor: pointer;
    font-weight: 600;
    list-style: none; /* remove default triangle in some browsers */
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  summary::after {
    content: "+";
    transition: transform 0.2s;
  }

  details[open] summary::after {
    transform: rotate(45deg);
  }

  details > :not(summary) {
    padding: 0 16px 14px;
  }
</style>
```

# Explanation

`<details>` and `<summary>` create a native disclosure widget — a collapsible section the user can open and close — with zero JavaScript. The browser handles the toggle behaviour, focus, keyboard interaction, and ARIA states automatically.

## Breakdown

- **`<details>`**  
  The outer container. Everything inside it except `<summary>` is the hidden content — collapsed by default, revealed when opened. Has an `open` property that toggles via JS or the `open` attribute in HTML.

- **`<summary>`**  
  The always-visible heading/label that the user clicks to toggle the details. If omitted, the browser provides a default label ("Details"). The first child of `<details>` — everything after it is the expandable content.

- **`open` attribute**  
  A boolean attribute on `<details>`. Present = expanded. Absent = collapsed. Can be toggled in JS: `el.open = true` / `el.open = false` / `el.toggleAttribute("open")`.

- **`toggle` event**  
  Fires on `<details>` when its state changes: `details.addEventListener("toggle", () => console.log(details.open))`. Useful for lazy-loading content on first open.

- **`name` attribute (accordion group)**  
  A newer HTML feature: multiple `<details>` elements sharing the same `name` form an **exclusive group** — opening one automatically closes all others. This is the native HTML accordion pattern, no JavaScript needed.

- **Browser-default disclosure triangle**  
  The default arrow/triangle next to `<summary>` is styled with `list-style-type` (Firefox) and `::webkit-details-marker` (Chrome). Hide both with `summary { list-style: none; }` and `summary::-webkit-details-marker { display: none; }` for full custom control.

- **`details[open] summary::after`**  
  A CSS pattern for a custom expand/collapse indicator. Style the `::after` pseudo-element on `<summary>` and apply different styles when the parent `<details>` has the `open` attribute.

## Key Points / Notes

- `<details>` and `<summary>` provide keyboard support for free — Enter and Space toggle the disclosure when focused.
- The `name` attribute for exclusive accordions is a relatively new HTML feature. Check current browser support if targeting older browsers.
- Unlike DIV-based accordions, `<details>` exposes proper accessibility semantics — screen readers announce it as a disclosure widget and read its expanded/collapsed state.
- Content inside closed `<details>` is still in the DOM and can be found by `Ctrl+F` in-page search — it will auto-expand if the browser finds the search term inside it.
- For animated open/close, CSS `transition` on `<details>` content requires some workarounds (height: 0 → auto doesn't animate). Modern CSS `interpolate-size: allow-keywords` or the View Transitions API are emerging solutions.
