```html
<head>

  <!-- Classic .ico — supported everywhere, should always exist -->
  <link rel="icon" href="/favicon.ico" sizes="any" />

  <!-- Modern PNG favicons — for better quality -->
  <link rel="icon" type="image/png" sizes="32x32"  href="/icons/favicon-32x32.png" />
  <link rel="icon" type="image/png" sizes="16x16"  href="/icons/favicon-16x16.png" />

  <!-- SVG favicon — scalable, great for modern browsers -->
  <link rel="icon" type="image/svg+xml" href="/icons/favicon.svg" />

  <!-- Apple Touch Icon — used when added to iOS home screen -->
  <link rel="apple-touch-icon" sizes="180x180" href="/icons/apple-touch-icon.png" />

  <!-- Android / Chrome — Web App Manifest -->
  <link rel="manifest" href="/site.webmanifest" />

  <!-- Windows tile color -->
  <meta name="msapplication-TileColor" content="#00add8" />

  <!-- Theme color for browser chrome -->
  <meta name="theme-color" content="#0d0f12" />

</head>
```

# Explanation

A favicon is the small icon shown in the browser tab, bookmark bar, search history, and when a user saves the page to their device's home screen. A complete favicon setup covers multiple sizes and formats across all platforms.

## Breakdown

- **`/favicon.ico`**  
  The original favicon format — a `.ico` file that can contain multiple resolutions (16×16 and 32×32) in one file. Browsers check for this at the root of the domain automatically. Always keep it there as a fallback.

- **`rel="icon" type="image/png"`**  
  PNG favicons at specific sizes. `32×32` is the standard browser tab size. `16×16` is used in some contexts. Better quality than `.ico` for non-legacy environments.

- **`rel="icon" type="image/svg+xml"`**  
  A single SVG file that scales perfectly to any size. Modern browsers (Chrome 80+, Firefox 41+, Safari 14+) support it. The recommended approach going forward — one file replaces all the PNGs.

- **`rel="apple-touch-icon"`**  
  The icon shown when a user adds the page to their iOS home screen. Must be PNG format. `180×180` is the recommended size for modern iPhones. No rounded corners needed — iOS applies them automatically.

- **`rel="manifest"`**  
  Links a JSON file (`site.webmanifest`) that describes the web app — name, icons, colors, display mode, and more. Used by Android Chrome and PWA (Progressive Web App) installers to configure the home screen experience.

- **`name="msapplication-TileColor"`**  
  The background color of the tile when the site is pinned to the Windows Start menu. Largely legacy (Internet Explorer / Edge legacy) but harmless to include.

- **`name="theme-color"`**  
  Sets the browser chrome color on mobile Chrome, Samsung Internet, and some other browsers. Creates a polished, branded feel.

## Key Points / Notes

- The minimum setup for most sites: a `favicon.ico` at the root + a `favicon.svg` + an `apple-touch-icon.png` at 180×180. That covers 95%+ of cases.
- SVG favicons can respond to dark mode: use `@media (prefers-color-scheme: dark)` inside the SVG's `<style>` to show different colors in dark mode.
- `site.webmanifest` is a plain JSON file. A minimal one includes `name`, `short_name`, `icons`, `theme_color`, `background_color`, and `display`. It enables Chrome on Android to prompt users to "Add to Home Screen."
- Don't hotlink favicons from another domain — they may change or disappear. Host your own copies.
- Favicon generators like `realfavicongenerator.net` can create all the necessary sizes and the `.webmanifest` from a single source image.
