```html
<!-- Basic image -->
<img src="photo.jpg" alt="A sunset over the mountains" />

<!-- Explicit dimensions prevent layout shift -->
<img src="avatar.png" alt="User profile photo" width="200" height="200" />

<!-- Lazy loading — defers until near viewport -->
<img src="article-photo.jpg" alt="Article illustration" loading="lazy" />

<!-- Responsive image with multiple sources -->
<img
  src="image-800.jpg"
  srcset="image-400.jpg 400w, image-800.jpg 800w, image-1600.jpg 1600w"
  sizes="(max-width: 600px) 400px, 800px"
  alt="Responsive landscape photo"
/>

<!-- Figure with caption -->
<figure>
  <img src="diagram.png" alt="System architecture diagram showing three layers" />
  <figcaption>Figure 1 — System architecture overview</figcaption>
</figure>

<!-- Decorative image — empty alt, ignored by screen readers -->
<img src="divider.svg" alt="" />
```

# Explanation

The `<img>` tag embeds images in a page. It is a **void element** — it has no closing tag and no content. The two required attributes are `src` (the image file) and `alt` (a description of it).

## Breakdown

- **`src`**  
  The path or URL of the image file. Can be relative (`images/photo.jpg`), root-relative (`/images/photo.jpg`), or absolute (`https://cdn.example.com/photo.jpg`).

- **`alt`**  
  Alternative text. Displayed when the image fails to load, read aloud by screen readers, and indexed by search engines. Describe what the image *shows* or *communicates*, not what it looks like technically.  
  - Informative image: describe its meaning in context.  
  - Decorative image: use `alt=""` (empty, not omitted — omitting it is an accessibility error).

- **`width` and `height`**  
  Setting both tells the browser the aspect ratio *before* the image loads, reserving the correct space. Prevents **Cumulative Layout Shift (CLS)** — content jumping as images load — which is a Google Core Web Vitals metric.

- **`loading="lazy"`**  
  Defers fetching the image until it's about to enter the viewport. Improves page load time for below-the-fold images. Never use on hero/banner images — use `loading="eager"` (or omit it) for above-the-fold content.

- **`srcset`**  
  A list of image source candidates at different sizes. The `w` descriptor is the image's actual pixel width. The browser picks the best candidate based on screen size and resolution.

- **`sizes`**  
  Tells the browser how wide the image will *render* at different viewport breakpoints. Works with `srcset`. Allows the browser to make the right choice before CSS is parsed.

- **`<figure>` and `<figcaption>`**  
  Semantic wrapper for self-contained media with an optional caption. A `<figure>` can be relocated in the document without breaking the surrounding content flow.

## Key Points / Notes

- `alt` is **not optional** — a missing `alt` attribute is an accessibility violation. An empty `alt=""` is correct for purely decorative images.
- Always specify `width` and `height` — preventing layout shift is a measurable, rankable performance metric.
- Format guide: **JPEG** for photos, **PNG** for transparency, **SVG** for icons/vector art, **WebP** for best modern compression.
- Use `loading="lazy"` on all images below the fold. For your hero/banner image, omit it — deferring it delays the most visible content on the page.
- Don't use `<img>` for decorative backgrounds. Use CSS `background-image` — those images are correctly skipped by screen readers.
