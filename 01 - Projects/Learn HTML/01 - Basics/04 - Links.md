```html
<!-- External link — opens in new tab -->
<a href="https://example.com" target="_blank" rel="noopener noreferrer">Visit Example</a>

<!-- Internal link — same site -->
<a href="/about">About Page</a>

<!-- Relative link — same directory -->
<a href="contact.html">Contact</a>

<!-- Anchor link — jump to section on the same page -->
<a href="#contact">Jump to Contact</a>
<section id="contact">...</section>

<!-- Email link -->
<a href="mailto:hello@example.com">Email Me</a>

<!-- Phone link -->
<a href="tel:+923001234567">Call Me</a>

<!-- Download link -->
<a href="/files/resume.pdf" download="Ammar-Resume.pdf">Download Resume</a>

<!-- Placeholder link -->
<a href="#">Placeholder</a>
```

# Explanation

The `<a>` (anchor) tag creates hyperlinks — the fundamental building block of the web. The `href` attribute defines where the link points. Without it, `<a>` renders as plain text with no link behaviour.

## Breakdown

- **`href`**  
  HyperText Reference — the destination. Can be an absolute URL, a root-relative path (`/page`), a relative path (`../page`), a fragment (`#id`), or a protocol (`mailto:`, `tel:`).

- **`target="_blank"`**  
  Opens the link in a new browser tab. Default (no `target`) opens in the current tab.

- **`rel="noopener noreferrer"`**  
  **Always required with `target="_blank"`**. Without it, the new tab can access the opener's `window` object — a security vulnerability called tabnabbing. `noopener` blocks that access; `noreferrer` also hides the HTTP referrer header.

- **`href="/about"` (root-relative)**  
  Always resolves relative to the domain root, regardless of the current page location. Reliable for site-wide navigation.

- **`href="contact.html"` (relative)**  
  Resolves relative to the current file's directory. Useful for small static sites where pages sit in the same folder.

- **`href="#section-id"` (fragment)**  
  Scrolls to the element with the matching `id`. The element must have `id="contact"` (no `#`). Used for in-page navigation and table of contents.

- **`href="mailto:..."`**  
  Opens the user's default email client. Can include subject and body: `mailto:a@b.com?subject=Hi&body=Hello`.

- **`href="tel:..."`**  
  Initiates a phone call on mobile. Always use international format with the `+` country code.

- **`download`**  
  Forces the browser to download the file instead of navigating to it. The value sets the saved filename. Without a value, the original filename is used.

## Key Points / Notes

- **Always** pair `target="_blank"` with `rel="noopener noreferrer"` — no exceptions.
- Link text must describe the destination: **"Read the documentation"** not **"Click here"** or **"Read more"** — screen readers read links in isolation.
- `<a>` is inline by default. Wrap a `<div>` or block content in `<a>` to make an entire card clickable — valid in HTML5.
- `href="#"` scrolls to the top of the page, which is jarring UX. Use `<button>` for non-navigating interactions.
- For keyboard accessibility, links are naturally focusable (Tab key) and activatable (Enter key) — no extra work needed.
