```html
<!-- <picture>: art direction — different image for different screens -->
<picture>
  <!-- Mobile: square crop -->
  <source media="(max-width: 600px)" srcset="hero-mobile.jpg" />

  <!-- Tablet: wider crop -->
  <source media="(max-width: 1024px)" srcset="hero-tablet.jpg" />

  <!-- Desktop: full panorama -->
  <img src="hero-desktop.jpg" alt="Mountain panorama at sunrise" width="1440" height="600" />
</picture>

<!-- <picture>: format selection — browser picks the best it supports -->
<picture>
  <source type="image/avif" srcset="photo.avif" />
  <source type="image/webp" srcset="photo.webp" />
  <img src="photo.jpg" alt="Portrait photo" width="800" height="600" loading="lazy" />
</picture>

<!-- Combining art direction + format selection -->
<picture>
  <source
    media="(max-width: 600px)"
    type="image/webp"
    srcset="hero-mobile.webp"
  />
  <source
    media="(max-width: 600px)"
    srcset="hero-mobile.jpg"
  />
  <source
    type="image/webp"
    srcset="hero-desktop.webp"
  />
  <img src="hero-desktop.jpg" alt="Hero image" width="1440" height="600" />
</picture>

<!-- srcset with w descriptors + sizes (resolution switching, no art direction) -->
<img
  src="photo-800.jpg"
  srcset="
    photo-400.jpg  400w,
    photo-800.jpg  800w,
    photo-1200.jpg 1200w,
    photo-1600.jpg 1600w
  "
  sizes="
    (max-width: 480px)  100vw,
    (max-width: 900px)  50vw,
    800px
  "
  alt="Responsive article image"
  width="800"
  height="533"
  loading="lazy"
/>

<!-- srcset with x descriptors — for high-DPI (retina) screens -->
<img
  src="logo.png"
  srcset="logo@2x.png 2x, logo@3x.png 3x"
  alt="Company Logo"
  width="120"
  height="40"
/>
```

# Explanation

`<picture>` and `srcset` are the two mechanisms for responsive images. `srcset` with `sizes` handles resolution switching (same image, different sizes). `<picture>` handles art direction (different images for different layouts) and format selection (AVIF, WebP, JPEG).

## Breakdown

- **`<picture>`**  
  A container that wraps one or more `<source>` elements and exactly one `<img>`. The browser evaluates the `<source>` conditions in order and uses the first match. The `<img>` is the required fallback for unsupported browsers and provides the alt text and dimensions.

- **`<source media="...">`**  
  Matches based on a CSS media query. When the viewport matches, the browser uses that source's `srcset`. Order matters — first match wins.

- **`<source type="...">`**  
  Matches based on whether the browser supports that image format. `image/avif`, `image/webp`, `image/jpeg`. The browser skips sources with unsupported types and falls through to the `<img>`.

- **`<img>` inside `<picture>`**  
  Always required — it's the fallback and the element that carries `alt`, `width`, `height`, `loading`, and `class`. The `src` attribute on this `<img>` is the ultimate fallback.

- **`srcset` with `w` descriptors**  
  A list of image sources with their intrinsic widths in pixels (`400w`, `800w`). The browser selects the best candidate based on the layout width from `sizes` and the screen's device pixel ratio.

- **`sizes`**  
  Tells the browser how wide the image will be rendered at different viewport sizes. Written as a list of media conditions and corresponding CSS lengths. The last value (no media condition) is the default. This is read before CSS loads — essential for the browser to make the right choice early.

- **`srcset` with `x` descriptors**  
  A list of candidates for different device pixel ratios. `2x` targets Retina/HiDPI screens (iPhone, MacBook Pro). `3x` targets very high density screens (iPhone Pro). Simpler than `w` + `sizes` but less flexible.

- **`image/avif`**  
  The newest and most efficient format. ~50% smaller than JPEG at same quality. Excellent browser support as of 2024. Always offer as the first `<source>`.

- **`image/webp`**  
  ~25–35% smaller than JPEG. Near-universal browser support. A strong second choice after AVIF.

## Key Points / Notes

- The `<img>` fallback is evaluated last. Put your most efficient, most compatible format first in `<picture>` (AVIF → WebP → JPEG).
- `sizes` describes the **layout** width, not the pixel width of the file. `100vw` means the image fills the full viewport width. The browser applies the device pixel ratio separately.
- Always include `width` and `height` on the `<img>` inside `<picture>` to prevent layout shift — even when the image dimensions may vary between sources.
- For art direction, the breakpoints in `<source media>` should mirror your CSS layout breakpoints so the image crop matches the layout change.
- Automate responsive image generation — manually exporting 4 sizes × 3 formats = 12 files per image. Tools like Sharp (Node.js), Cloudinary, or build-time plugins handle this automatically.
