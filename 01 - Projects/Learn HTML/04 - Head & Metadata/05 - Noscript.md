```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Page with Noscript</title>

  <!-- <noscript> in <head> — can only contain <link>, <style>, or <meta> -->
  <noscript>
    <style>
      /* Hide JS-dependent elements when JS is disabled */
      .js-only { display: none; }
      .no-js-warning { display: block; }
    </style>
    <link rel="stylesheet" href="no-js-fallback.css" />
  </noscript>

</head>
<body>

  <!-- <noscript> in <body> — can contain any HTML -->
  <noscript>
    <div class="no-js-banner">
      <strong>JavaScript is disabled.</strong>
      Some features on this page require JavaScript to work.
      Please enable it in your browser settings for the full experience.
    </div>
  </noscript>

  <!-- JavaScript-rendered content -->
  <div id="app">
    <!-- React / Vue / etc. renders here -->
  </div>

  <!-- Fallback content for users without JS -->
  <noscript>
    <main>
      <h1>Articles</h1>
      <ul>
        <li><a href="/articles/html-basics">HTML Basics</a></li>
        <li><a href="/articles/css-intro">CSS Introduction</a></li>
      </ul>
    </main>
  </noscript>

  <!-- Analytics that only fire when JS is enabled -->
  <script>
    // Google Analytics or similar
    gtag("config", "GA_MEASUREMENT_ID");
  </script>

  <!-- Pixel fallback when JS is disabled -->
  <noscript>
    <img
      src="https://analytics.example.com/pixel?page=home"
      alt=""
      width="1"
      height="1"
      style="display:none"
    />
  </noscript>

</body>
</html>
```

# Explanation

`<noscript>` defines fallback content that is rendered **only when JavaScript is disabled** in the browser, or when the browser doesn't support JavaScript at all. It provides a graceful degradation path for JS-dependent pages and features.

## Breakdown

- **`<noscript>` in `<head>`**  
  When placed in `<head>`, it can only contain `<link>`, `<style>`, and `<meta>` elements. Used to inject a fallback stylesheet or meta redirect when JavaScript is off. The content is ignored entirely when JS is enabled.

- **`<noscript>` in `<body>`**  
  When placed in `<body>`, it can contain any HTML content. Typically used to display a warning message, a static fallback, or a navigation structure for users without JavaScript.

- **Warning banner**  
  The most common use — a prominent message telling users that JavaScript is required or that some features won't work. Include a link to browser instructions if needed.

- **Static content fallback**  
  For Single Page Applications (React, Vue, Angular) that render entirely via JavaScript, `<noscript>` provides a static HTML version of the page's core content so users with JS disabled aren't left with a blank page.

- **CSS in `<noscript>`**  
  The `<style>` block inside `<noscript>` (in `<head>`) only applies when JS is disabled. Useful for showing `.no-js-warning` elements and hiding `.js-only` elements that have no non-JS equivalent.

- **Tracking pixel fallback**  
  Some analytics tools use a `<noscript>` image pixel as a fallback when JavaScript-based tracking can't run. The 1×1 transparent image fires an HTTP request to the analytics server when the `<noscript>` is rendered (i.e., when JS is disabled).

- **When `<noscript>` is rendered**  
  - JavaScript is disabled in browser settings.  
  - The browser doesn't support JavaScript (rare today).  
  - A browser extension blocks JavaScript execution.  
  - The `<script>` tag itself fails to load (network error) — note: `<noscript>` does NOT trigger in this case. It is specifically for when JS is disabled, not when a script errors.

## Key Points / Notes

- `<noscript>` does NOT trigger when a script throws a runtime error or fails to load — it only activates when JavaScript is entirely disabled. Use `try/catch` and error boundaries for runtime failures.
- The percentage of users with JavaScript disabled is very small (< 0.2% in most surveys), but it includes web crawlers, accessibility tools, and some corporate security environments.
- For SEO: Google does execute JavaScript for crawling, but `<noscript>` content is also indexed. In some architectures, important content is placed in both the rendered JS output and a `<noscript>` fallback to ensure it's indexed.
- `<noscript>` is a good signal that you've thought about progressive enhancement — building a functional base experience in HTML, then enhancing with JavaScript on top.
- In modern frameworks: Next.js, Nuxt, SvelteKit, and similar server-side-rendering frameworks reduce the need for `<noscript>` by rendering the initial HTML on the server. The page is functional even before JS loads.
