```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
    <p>This is my first HTML page.</p>
  </body>
</html>
```

# Explanation

This is the skeleton every HTML document must have. It tells the browser what kind of document it is, what language it's in, how to encode characters, and where the visible content lives.

## Breakdown

- **`<!DOCTYPE html>`**  
  Not a tag — an instruction to the browser to render the page in standards mode (HTML5). Always the very first line, before everything else.

- **`<html lang="en">`**  
  The root element that wraps the entire document. The `lang` attribute declares the page language for screen readers and search engines.

- **`<head>`**  
  A container for metadata — information *about* the page that isn't shown directly. Holds `<title>`, `<meta>`, `<link>`, `<script>`, and `<style>` tags.

- **`<meta charset="UTF-8">`**  
  Sets character encoding to UTF-8, which supports every language and emoji. Without it, special characters may render as garbage.

- **`<meta name="viewport" ...>`**  
  Critical for responsive design. Prevents mobile browsers from zooming the page out to fit — the page width matches the device screen width.

- **`<title>`**  
  The text shown in the browser tab and in search engine results. Every page must have a unique, descriptive title.

- **`<body>`**  
  Contains all visible content — text, images, links, forms — everything the user actually sees and interacts with.

## Key Points / Notes

- `<!DOCTYPE html>` must be the absolute first thing in the file — no whitespace or characters before it.
- A valid page has exactly **one** `<html>`, **one** `<head>`, and **one** `<body>`.
- The `lang` attribute on `<html>` matters for accessibility and SEO — always include it.
- `<head>` content is never rendered visually, but it controls how the page behaves, looks, and ranks.
- Omitting `<meta charset="UTF-8">` causes emoji and non-ASCII characters to display incorrectly.
