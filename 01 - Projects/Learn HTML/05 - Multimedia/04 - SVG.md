```html
<!-- Inline SVG — fully controllable with CSS and JS -->
<svg
  xmlns="http://www.w3.org/2000/svg"
  width="200"
  height="200"
  viewBox="0 0 200 200"
  role="img"
  aria-label="Blue circle"
>
  <circle cx="100" cy="100" r="80" fill="steelblue" stroke="#fff" stroke-width="4" />
</svg>

<!-- Common SVG shapes -->
<svg xmlns="http://www.w3.org/2000/svg" width="400" height="200" viewBox="0 0 400 200">
  <rect x="10"  y="10"  width="100" height="80" rx="8" fill="#00ADD8" />
  <circle cx="200" cy="50" r="40" fill="#3DDC84" />
  <ellipse cx="330" cy="50" rx="60" ry="40" fill="#F0C040" />
  <line x1="10" y1="150" x2="390" y2="150" stroke="#999" stroke-width="2" />
  <polyline points="10,190 100,140 200,170 300,120 390,160" fill="none" stroke="#FF5F6D" stroke-width="2" />
  <polygon points="200,110 240,180 160,180" fill="#C592EA" />
  <text x="10" y="195" font-size="14" fill="#ccc">SVG shapes</text>
</svg>

<!-- Path — the most powerful SVG element -->
<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100" viewBox="0 0 100 100">
  <path
    d="M 10 80 C 40 10, 65 10, 95 80 S 150 150, 180 80"
    fill="none"
    stroke="steelblue"
    stroke-width="3"
  />
</svg>

<!-- SVG icon with currentColor — inherits text color from CSS -->
<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" aria-hidden="true">
  <path d="M12 2L2 7l10 5 10-5-10-5zM2 17l10 5 10-5M2 12l10 5 10-5"
        stroke="currentColor" stroke-width="2" stroke-linecap="round" />
</svg>

<!-- SVG as <img> — simpler but can't be styled -->
<img src="logo.svg" alt="Company Logo" width="120" height="40" />
```

# Explanation

SVG (Scalable Vector Graphics) defines images using XML-based shapes and paths rather than pixels. Because SVG is vector-based, it scales perfectly to any size with no loss of quality — making it the ideal format for icons, logos, and illustrations.

## Breakdown

- **`xmlns`**  
  The XML namespace declaration. Required when SVG is used as a standalone file or in some HTML contexts. Can be omitted in modern inline HTML5.

- **`viewBox="minX minY width height"`**  
  Defines the internal coordinate system. `0 0 200 200` means the canvas runs from (0,0) to (200,200). The element's `width`/`height` attributes control the rendered size — the SVG scales its internal coordinates to fit. This is what makes SVG scalable.

- **`<rect>`**  
  A rectangle. `x`, `y` is the top-left corner. `width`, `height` define size. `rx`/`ry` round the corners.

- **`<circle>`**  
  A circle. `cx`, `cy` is the center point. `r` is the radius.

- **`<ellipse>`**  
  An ellipse. `cx`, `cy` is center. `rx` is horizontal radius, `ry` is vertical radius.

- **`<line>`**  
  A straight line from (`x1`, `y1`) to (`x2`, `y2`).

- **`<polyline>`**  
  A series of connected straight lines. `points` is a list of `x,y` coordinate pairs. Open shape (not closed).

- **`<polygon>`**  
  Like `<polyline>` but automatically closes the shape by connecting the last point back to the first.

- **`<text>`**  
  Renders text inside SVG. Can be positioned, styled, and animated like other SVG elements.

- **`<path>`**  
  The most powerful SVG element. The `d` attribute contains path commands: `M` (move to), `L` (line to), `C` (cubic bezier), `S` (smooth bezier), `A` (arc), `Z` (close). Most complex SVG shapes are paths.

- **`currentColor`**  
  A special CSS keyword that inherits the element's `color` property. Using `stroke="currentColor"` on an icon makes it automatically match the surrounding text color — no need to hardcode colors in the SVG.

- **`role="img"` and `aria-label`**  
  For meaningful inline SVGs, add these to give it an accessible name. For decorative icons, use `aria-hidden="true"` to hide it from screen readers entirely.

## Key Points / Notes

- Inline SVG (`<svg>` directly in HTML) is the most flexible method — styleable with CSS, animatable with CSS/JS, and no extra HTTP request.
- `<img src="file.svg">` is simpler but the SVG is isolated — you can't style its internals with your page's CSS. Good for logos where you don't need CSS control.
- Use `currentColor` for all icon SVGs — it makes them work correctly in any color scheme (dark mode, hover states, disabled states) with zero extra CSS.
- `viewBox` without `width`/`height` on the `<svg>` makes it fill its container — useful for responsive SVGs.
- SVG files can be minified (tools like SVGO remove unnecessary attributes and path data) to significantly reduce file size without any visual change.
