```html
<!-- YouTube embed -->
<iframe
  width="560"
  height="315"
  src="https://www.youtube-nocookie.com/embed/VIDEO_ID"
  title="Introduction to HTML — YouTube"
  frameborder="0"
  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share"
  allowfullscreen
  loading="lazy"
></iframe>

<!-- Google Maps embed -->
<iframe
  src="https://www.google.com/maps/embed?pb=..."
  width="600"
  height="450"
  style="border:0;"
  allowfullscreen
  loading="lazy"
  referrerpolicy="no-referrer-when-downgrade"
  title="Office location on Google Maps"
></iframe>

<!-- Embedding another page from the same site -->
<iframe
  src="/preview/article.html"
  width="100%"
  height="400"
  title="Article preview"
  sandbox="allow-scripts allow-same-origin"
></iframe>

<!-- Stripe payment form embed (third-party) -->
<iframe
  src="https://checkout.stripe.com/..."
  title="Secure payment form"
  sandbox="allow-forms allow-scripts allow-same-origin allow-popups"
></iframe>
```

# Explanation

`<iframe>` (inline frame) embeds an entirely separate HTML document inside the current page. It creates a completely isolated browsing context — the embedded content has its own DOM, stylesheets, and scripts. The primary use cases are embedding third-party content like YouTube, Google Maps, Stripe, and Codepen.

## Breakdown

- **`src`**  
  The URL of the document to embed. Can be from the same origin or a different one (subject to the target site allowing it via headers).

- **`title`**  
  **Required for accessibility.** Describes the iframe's content for screen readers — "YouTube video player" or "Google Maps showing office location." Without it, screen reader users have no idea what the frame contains.

- **`width` and `height`**  
  Dimensions of the iframe viewport in pixels (or CSS). Set to match your expected layout to avoid resizing jumps.

- **`frameborder="0"`**  
  Removes the default border drawn around the iframe. Deprecated in HTML5 (use `border: 0` in CSS instead) but still universally used in embed codes.

- **`allow`**  
  Grants specific browser features to the embedded content. YouTube requires `autoplay`, `clipboard-write`, `encrypted-media`, `gyroscope`, `picture-in-picture`. Each feature must be explicitly granted — the iframe doesn't inherit the parent page's permissions.

- **`allowfullscreen`**  
  Permits the embedded content to use the browser's fullscreen API. Required for YouTube's fullscreen button to work.

- **`loading="lazy"`**  
  Defers loading the iframe until it's near the viewport. Especially useful for embeds that are far down the page — iframes can be very heavy (YouTube loads ~400KB of JS).

- **`sandbox`**  
  Applies security restrictions to the embedded content. By default, `sandbox` blocks everything — scripts, forms, same-origin access, popups. Add back only the permissions you need:  
  - `allow-scripts` — run JavaScript  
  - `allow-forms` — submit forms  
  - `allow-same-origin` — preserve origin (needed for cookies, localStorage)  
  - `allow-popups` — open new windows  

- **`referrerpolicy`**  
  Controls how much referrer information is sent when the iframe loads its content. `no-referrer-when-downgrade` is a common safe default.

## Key Points / Notes

- Always add a descriptive `title` attribute to every `<iframe>` — it's an accessibility requirement (WCAG 2.4.1).
- Use `youtube-nocookie.com` instead of `youtube.com` for YouTube embeds to avoid setting tracking cookies until the user interacts with the video.
- `<iframe>` content cannot be styled with the parent page's CSS — each frame has complete style isolation. This is by design.
- `sandbox` without any `allow-*` values is the most restrictive setting. Use it for displaying untrusted HTML content safely.
- For iframes that need to match their content height dynamically (like an embedded comment section), you need JavaScript `postMessage` communication between the parent and the frame — there's no pure HTML solution.
