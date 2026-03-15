```html
<!-- Canvas element — drawn entirely via JavaScript -->
<canvas
  id="myCanvas"
  width="600"
  height="400"
  aria-label="A bar chart showing monthly revenue"
  role="img"
>
  <!-- Fallback for browsers that don't support canvas -->
  <p>Your browser does not support canvas. Here is the data as a table instead.</p>
</canvas>

<script>
  const canvas = document.getElementById("myCanvas");
  const ctx    = canvas.getContext("2d");

  // --- Shapes ---
  ctx.fillStyle = "#0d0f12";
  ctx.fillRect(0, 0, 600, 400);         // filled rectangle (x, y, w, h)

  ctx.strokeStyle = "#00ADD8";
  ctx.lineWidth = 3;
  ctx.strokeRect(50, 50, 100, 80);      // outlined rectangle

  ctx.clearRect(60, 60, 30, 30);        // erase a rectangle

  // --- Path ---
  ctx.beginPath();
  ctx.moveTo(200, 50);
  ctx.lineTo(350, 50);
  ctx.lineTo(275, 180);
  ctx.closePath();
  ctx.fillStyle = "#C592EA";
  ctx.fill();
  ctx.strokeStyle = "#fff";
  ctx.stroke();

  // --- Circle / Arc ---
  ctx.beginPath();
  ctx.arc(480, 100, 60, 0, Math.PI * 2);  // (x, y, radius, startAngle, endAngle)
  ctx.fillStyle = "#3DDC84";
  ctx.fill();

  // --- Text ---
  ctx.font = "bold 20px JetBrains Mono, monospace";
  ctx.fillStyle = "#dce3ee";
  ctx.fillText("Canvas Demo", 50, 300);

  // --- Image ---
  const img = new Image();
  img.onload = () => ctx.drawImage(img, 400, 250, 150, 100);
  img.src = "photo.jpg";

  // --- Gradient ---
  const grad = ctx.createLinearGradient(0, 350, 600, 350);
  grad.addColorStop(0,   "#00ADD8");
  grad.addColorStop(1,   "#C592EA");
  ctx.fillStyle = grad;
  ctx.fillRect(50, 340, 500, 20);
</script>
```

# Explanation

`<canvas>` provides a pixel-based drawing surface that is entirely controlled by JavaScript. Unlike SVG, canvas has no DOM — you draw onto a bitmap and it stays there until overwritten. It's used for games, image editors, data visualizations, and animations.

## Breakdown

- **`<canvas id width height>`**  
  The element creates a blank transparent bitmap. `width` and `height` set the pixel resolution of the drawing buffer — always set these in HTML attributes, not CSS, to avoid scaling artefacts.

- **`getContext("2d")`**  
  Returns the 2D rendering context — the object with all drawing methods. (Other contexts exist: `"webgl"` / `"webgl2"` for 3D graphics, `"bitmaprenderer"` for off-screen rendering.)

- **`fillRect(x, y, w, h)`**  
  Draws a filled rectangle. `fillStyle` sets the color, gradient, or pattern used.

- **`strokeRect(x, y, w, h)`**  
  Draws only the outline of a rectangle using `strokeStyle` and `lineWidth`.

- **`clearRect(x, y, w, h)`**  
  Erases pixels in the given area, making them transparent. The primary way to "clear" the canvas for animation frames.

- **`beginPath()` / `moveTo()` / `lineTo()` / `closePath()`**  
  Path commands for drawing arbitrary shapes. `beginPath` starts a new path. `moveTo` lifts the pen. `lineTo` draws to a point. `closePath` connects back to the start.

- **`fill()` / `stroke()`**  
  `fill()` paints the interior of the current path. `stroke()` draws the outline. Call after defining the path.

- **`arc(x, y, r, startAngle, endAngle)`**  
  Draws a circular arc. Angles are in radians — `0` is 3 o'clock, `Math.PI * 2` is a full circle. Use for circles, pie slices, and rounded caps.

- **`fillText(text, x, y)`**  
  Renders text on the canvas. Set `ctx.font` first. Unlike HTML text, canvas text is not selectable or accessible — it becomes pixels.

- **`drawImage(img, x, y, w, h)`**  
  Draws an `Image`, another `<canvas>`, or a `<video>` frame onto the canvas. The image must be loaded first (use the `onload` callback).

- **`createLinearGradient(x1, y1, x2, y2)`**  
  Creates a gradient between two points. Add color stops with `.addColorStop(position, color)` where position is `0` (start) to `1` (end).

## Key Points / Notes

- Canvas is **pixel-based** — once drawn, content has no memory. Interactivity requires redrawing everything each frame and using math to detect pointer position over shapes.
- SVG vs Canvas: use SVG for scalable, accessible, static or simply animated graphics. Use Canvas for performance-heavy rendering (hundreds of objects, video processing, games).
- Canvas content is **not accessible** by default. Add `role="img"` and `aria-label` for meaningful canvases. For complex charts, provide a data table as a text alternative.
- For animation, use `requestAnimationFrame` — not `setInterval`. It syncs to the display refresh rate and pauses when the tab is not visible (saving CPU/battery).
- The `width` and `height` attributes on `<canvas>` set the drawing buffer resolution. Setting these via CSS instead will stretch the existing buffer, resulting in blurry output. Always set them as HTML attributes.
