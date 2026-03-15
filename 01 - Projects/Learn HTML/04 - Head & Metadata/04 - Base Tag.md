```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- base: sets the base URL for all relative links on the page -->
  <base href="https://example.com/docs/" />

  <!-- base with target: sets default link target for all links -->
  <base href="https://example.com/" target="_blank" />

  <title>Page with Base Tag</title>
</head>
<body>

  <!-- Without <base>: resolves to the current page's directory -->
  <!-- With <base href="https://example.com/docs/">: resolves to https://example.com/docs/intro.html -->
  <a href="intro.html">Introduction</a>

  <!-- With base: https://example.com/docs/images/logo.png -->
  <img src="images/logo.png" alt="Logo" />

  <!-- Absolute URLs are NOT affected by <base> -->
  <a href="https://other-site.com">Not affected</a>

  <!-- Fragment links are affected — use absolute path to avoid issues -->
  <!-- ❌ With <base>, this resolves to https://example.com/docs/#section -->
  <!-- not the current page's #section -->
  <a href="#section">Jump to section</a>

  <!-- ✅ Fix: use the full page URL for fragment links -->
  <a href="https://example.com/docs/page.html#section">Jump to section</a>

</body>
</html>
```

# Explanation

The `<base>` element sets a base URL that all **relative** URLs on the page resolve against. It also sets a default `target` for all links. There can only be one `<base>` element per page, and it must be in `<head>` before any other elements that reference URLs.

## Breakdown

- **`href` attribute**  
  The base URL. All relative URLs on the page (`href`, `src`, `action`, `srcset`) are resolved relative to this URL instead of the page's actual URL. Must be an absolute URL. Ends with `/` if you want relative paths to extend from a directory.

- **`target` attribute**  
  Sets the default browsing context for all links that don't have their own `target`. `"_blank"` makes every link open in a new tab by default. Can be overridden by setting `target` directly on individual `<a>` tags.

- **How URL resolution works**  
  Without `<base>`: `href="page.html"` resolves relative to the current page's directory.  
  With `<base href="https://example.com/docs/">`: `href="page.html"` resolves to `https://example.com/docs/page.html`.  
  Absolute URLs (starting with `https://`) are always unaffected by `<base>`.

- **Fragment links and `<base>` — the big gotcha**  
  `href="#section"` is a relative URL. With `<base>`, it resolves to `base-url#section` — pointing to a fragment on the *base URL*, not the current page. This breaks in-page navigation. Fix: use the full current page URL: `href="https://example.com/current-page.html#section"`.

- **Only one `<base>` per page**  
  If multiple `<base>` elements appear, only the first `href` and first `target` are used. Duplicates are ignored.

- **Must appear in `<head>` before other resource-referencing elements**  
  The `<base>` tag must come before any element that uses URLs — `<link>`, `<script>`, `<img>`, etc. — so those URLs resolve against the base correctly.

## Key Points / Notes

- `<base>` is useful for sites where pages are loaded as templates into a different URL context (e.g., a CMS injecting content into a different path, or HTML email templates where relative paths need a known base).
- For most modern web apps built with absolute paths or a bundler, `<base>` is unnecessary and rarely used.
- The fragment link gotcha is the most common and confusing bug caused by `<base>`. If you use `<base>`, audit every `href="#..."` on the page.
- When `<base target="_blank">` is set, every link on the page opens in a new tab unless individually overridden. This is aggressive UX — use it only when the entire page is meant to be a launcher for external content.
- `<base>` affects `<form action="...">` too — relative form action URLs resolve against the base, which may send data to the wrong endpoint if you're not careful.
