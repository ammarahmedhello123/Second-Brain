```html
<head>
  <!-- External CSS stylesheet -->
  <link rel="stylesheet" href="styles.css" />

  <!-- Multiple stylesheets -->
  <link rel="stylesheet" href="reset.css" />
  <link rel="stylesheet" href="typography.css" />
  <link rel="stylesheet" href="components.css" />

  <!-- CSS for a specific media type -->
  <link rel="stylesheet" href="print.css" media="print" />

  <!-- Preload a critical CSS file for performance -->
  <link rel="preload" href="critical.css" as="style" onload="this.rel='stylesheet'" />

  <!-- Google Fonts (external font import) -->
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Inter:wght@400;700&display=swap" />

  <!-- Inline CSS (avoid except for critical styles) -->
  <style>
    body { margin: 0; font-family: sans-serif; }
  </style>

</head>
<body>

  <!-- External JS — defer: parsed after HTML, in order -->
  <script src="app.js" defer></script>

  <!-- External JS — async: fetched in parallel, runs ASAP -->
  <script src="analytics.js" async></script>

  <!-- Module script -->
  <script type="module" src="main.js"></script>

  <!-- Inline JS (avoid except for small critical snippets) -->
  <script>
    console.log("Page loaded");
  </script>

</body>
```

# Explanation

The `<link>` element connects external resources to the page. The `<script>` element loads or embeds JavaScript. The placement and attributes of both directly impact page load speed and rendering order.

## Breakdown

- **`<link rel="stylesheet" href="...">`**  
  Links an external CSS file. The browser fetches it and blocks rendering until it's parsed (CSS is render-blocking). Place all stylesheets in `<head>` so styles are ready when the HTML is parsed.

- **`media="print"`**  
  Loads the stylesheet only when the page is being printed. `media="screen"` for displays, `media="(max-width: 600px)"` for responsive breakpoints (though CSS media queries inside the file are more common).

- **`rel="preconnect"`**  
  Tells the browser to establish a connection (DNS lookup, TCP handshake, TLS) to a domain early — before the actual resource is requested. Reduces latency for external fonts and CDN resources.

- **`<style>`**  
  Inline CSS directly in the HTML. Use only for truly critical above-the-fold styles (to eliminate a render-blocking request). Avoid for general styling — it can't be cached and mixes concerns.

- **`<script src="..." defer>`**  
  Fetches the JS file in parallel with HTML parsing, but only runs it after the HTML is fully parsed. Scripts execute in source order. **Best choice for most scripts.** Eliminates the need to place scripts at the bottom of `<body>`.

- **`<script src="..." async>`**  
  Fetches the JS file in parallel and runs it immediately when downloaded — potentially before HTML is done parsing. Scripts do NOT execute in order. Use only for independent scripts like analytics that have no dependencies.

- **`<script type="module">`**  
  Loads the script as an ES module. Automatically deferred. Enables `import`/`export` syntax. Runs in strict mode. Has its own scope (variables are not global by default).

- **Inline `<script>`**  
  JavaScript embedded directly in HTML. No network request needed. Use for tiny critical snippets (e.g., dark mode detection before paint). For anything substantial, use external files — they can be cached.

## Key Points / Notes

- CSS `<link>` tags go in `<head>`. JavaScript `<script>` tags can go in `<head>` (with `defer` or `async`) or at the end of `<body>`. A script without `defer`/`async` in `<head>` blocks HTML parsing — avoid it.
- `defer` vs `async`: use `defer` for scripts that manipulate the DOM or depend on other scripts. Use `async` for independent scripts (analytics, ads) that don't care when they run.
- Multiple CSS files = multiple network requests. In production, bundle them into one file or use HTTP/2 which handles multiple requests efficiently.
- `rel="preconnect"` for Google Fonts is important — it pre-warms the connection before the browser discovers the font URL, reducing visible font loading delay.
- The `crossorigin` attribute on `<link rel="preconnect">` is required when the resource uses CORS (Cross-Origin Resource Sharing) — like Google Fonts' font files from `fonts.gstatic.com`.
