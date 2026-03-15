```html
<!DOCTYPE html>
<html lang="en">
<head>
  <!-- 1. charset and viewport first -->
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- 2. DNS prefetch / preconnect for external resources -->
  <link rel="preconnect"    href="https://fonts.googleapis.com" />
  <link rel="preconnect"    href="https://fonts.gstatic.com" crossorigin />
  <link rel="dns-prefetch"  href="https://cdn.example.com" />

  <!-- 3. Preload critical resources -->
  <link rel="preload" href="/fonts/MyFont.woff2" as="font" type="font/woff2" crossorigin />
  <link rel="preload" href="/hero.jpg" as="image" />

  <!-- 4. CSS in <head> — render-blocking on purpose -->
  <link rel="stylesheet" href="styles.css" />

  <title>Performant Page</title>
</head>
<body>

  <!-- 5. Hero image: no lazy loading, explicit dimensions, modern formats -->
  <picture>
    <source type="image/avif" srcset="hero.avif" />
    <source type="image/webp" srcset="hero.webp" />
    <img
      src="hero.jpg"
      alt="Hero image"
      width="1440" height="600"
      fetchpriority="high"
    />
  </picture>

  <!-- 6. Below-fold images: lazy load -->
  <img
    src="article-photo.jpg"
    alt="Article illustration"
    width="800" height="500"
    loading="lazy"
    decoding="async"
  />

  <!-- 7. Deferred iframes -->
  <iframe
    src="https://www.youtube-nocookie.com/embed/ID"
    title="Video"
    loading="lazy"
    width="560" height="315"
  ></iframe>

  <!-- 8. JS at the bottom — or use defer/async in <head> -->
  <script src="app.js" defer></script>
  <script src="analytics.js" async></script>

</body>
</html>
```

# Explanation

HTML performance isn't just about JavaScript bundles and CSS files — the HTML itself controls *when* and *in what order* the browser fetches, parses, and renders resources. The right HTML decisions can dramatically reduce the time to first meaningful paint.

## Breakdown

- **`<meta charset>` and `<meta viewport>` first**  
  Both must be parsed immediately. `charset` before any text is decoded. `viewport` before layout calculations. Any delay causes incorrect initial rendering.

- **`rel="preconnect"`**  
  Initiates the TCP connection (and TLS handshake for HTTPS) to an external domain before the browser discovers a resource from that domain. Typically saves 100–300ms for fonts and CDN assets.

- **`rel="dns-prefetch"`**  
  A lighter version of `preconnect` — resolves only the DNS. Useful for domains you don't need immediately but will need soon.

- **`rel="preload"`**  
  Tells the browser to fetch a specific resource as soon as possible, before the parser would normally discover it. Use for: hero images, critical fonts, key scripts. Always include `as` (the resource type) and `crossorigin` for fonts.

- **CSS in `<head>`**  
  CSS is render-blocking intentionally — you want styles applied before any content is displayed, preventing a flash of unstyled content (FOUC). Keep critical CSS small.

- **`fetchpriority="high"`**  
  Hints to the browser that this resource should be fetched with high priority. Use on the hero/LCP (Largest Contentful Paint) image to ensure it loads as early as possible.

- **`loading="lazy"` on below-fold images**  
  Defers network requests for images not yet visible, reducing initial page load time and data usage.

- **`decoding="async"`**  
  Allows the browser to decode the image off the main thread, reducing jank. Safe to use on all images. `decoding="sync"` (default) blocks the main thread during decode.

- **`<script defer>`**  
  Downloads the script in parallel with HTML parsing and runs it after the DOM is complete. In-order execution. Best default for app scripts.

- **`<script async>`**  
  Downloads in parallel and runs immediately when ready — potentially before DOM is complete. No order guarantee. Best for independent third-party scripts (analytics, ads).

## Key Points / Notes

- The **LCP (Largest Contentful Paint)** element — usually the hero image — should never have `loading="lazy"`. Use `fetchpriority="high"` instead to promote it.
- Measure performance with Lighthouse (Chrome DevTools → Lighthouse tab). The key metrics are LCP, CLS (Cumulative Layout Shift), and INP (Interaction to Next Paint).
- Prevent CLS by always providing `width` and `height` on `<img>` and `<iframe>`. The browser uses these to reserve space before the resource loads.
- `<link rel="preload">` is a commitment — every preloaded resource must be used on the page. Unused preloads are a performance warning in Lighthouse.
- Load order summary: `charset` → `viewport` → `preconnect` → `preload` → critical CSS → body content → below-fold lazy images → `<script defer>` at end of body.
