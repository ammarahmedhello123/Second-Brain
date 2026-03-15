```html
<!-- datalist — native autocomplete suggestions for an input -->
<label for="browser">Favourite Browser</label>
<input type="text" id="browser" name="browser" list="browsers" />
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Safari">
  <option value="Edge">
  <option value="Brave">
  <option value="Arc">
</datalist>

<!-- datalist with email suggestions -->
<input type="email" name="email" list="email-suggestions" />
<datalist id="email-suggestions">
  <option value="me@gmail.com">
  <option value="work@company.com">
</datalist>

<!-- datalist with numeric range hints -->
<label for="temp">Temperature (°C)</label>
<input type="range" id="temp" name="temp" min="0" max="100" list="temps" />
<datalist id="temps">
  <option value="0"   label="Freezing">
  <option value="20"  label="Room temp">
  <option value="37"  label="Body temp">
  <option value="100" label="Boiling">
</datalist>

<!-- ─────────────────────────────────────────── -->

<!-- progress — completion of a task (0 to max) -->

<!-- Determinate: known percentage -->
<label for="upload">Uploading file...</label>
<progress id="upload" value="65" max="100">65%</progress>

<!-- Indeterminate: unknown duration (no value attribute) -->
<progress>Loading...</progress>

<!-- Updating progress via JavaScript -->
<progress id="task-bar" value="0" max="100"></progress>
<button onclick="startProgress()">Start</button>
<script>
  function startProgress() {
    const bar = document.getElementById("task-bar");
    let val = 0;
    const interval = setInterval(() => {
      val += 10;
      bar.value = val;
      if (val >= 100) clearInterval(interval);
    }, 300);
  }
</script>

<!-- ─────────────────────────────────────────── -->

<!-- meter — a scalar measurement within a known range -->

<!-- Disk usage -->
<label for="disk">Disk Usage</label>
<meter id="disk" value="7.5" min="0" max="10" low="3" high="8" optimum="2">
  7.5 GB of 10 GB used
</meter>

<!-- Score / grade -->
<meter value="0.72" min="0" max="1" low="0.4" high="0.7" optimum="1">72%</meter>

<!-- Battery level -->
<meter value="35" min="0" max="100" low="20" high="80" optimum="100">35%</meter>

<!-- ─────────────────────────────────────────── -->

<!-- output — result of a calculation -->
<form oninput="result.value = parseInt(a.value) + parseInt(b.value)">
  <label for="a">First number</label>
  <input type="number" id="a" name="a" value="10" />

  <span>+</span>

  <label for="b">Second number</label>
  <input type="number" id="b" name="b" value="5" />

  <span>=</span>

  <output name="result" for="a b">15</output>
</form>
```

# Explanation

These four elements extend HTML forms with native interactivity — suggestions without JavaScript (`<datalist>`), progress display (`<progress>`), scalar gauges (`<meter>`), and calculated results (`<output>`). They cover common UI patterns that previously required custom implementations.

## Breakdown

- **`<datalist>`**  
  Provides a list of suggested values for an `<input>`. The input and datalist are linked by matching the input's `list` attribute to the datalist's `id`. Unlike `<select>`, the user can still type freely and ignore the suggestions. Works with `type="text"`, `"email"`, `"url"`, `"tel"`, `"number"`, `"range"`, and date types.

- **`<option>` inside `<datalist>`**  
  Each `<option>` is a suggestion. Only the `value` attribute matters — the displayed suggestion is the `value`. The `label` attribute adds a secondary description shown alongside the value in some browsers.

- **`<progress value max>`**  
  Displays a progress bar for a task with a definite (known) or indefinite (unknown) completion point.  
  - **Determinate**: set both `value` (current) and `max` (total). Renders a filled bar proportional to `value / max`.  
  - **Indeterminate**: omit `value` (keep only `max` or omit both). Renders an animated "loading" bar.  
  The content between tags is the fallback for browsers that don't support it.

- **`<meter value min max low high optimum>`**  
  A gauge for a scalar measurement within a known range — disk usage, password strength, test score, battery level. Not for task progress — use `<progress>` for that.  
  - `min` / `max` — the full range.  
  - `low` — values below this are "low" (may color amber/red).  
  - `high` — values above this are "high" (may color amber/red).  
  - `optimum` — the ideal/preferred value. If `optimum` is below `low`, then low values are green; if above `high`, then high values are green. The browser determines color automatically.

- **`<output name for>`**  
  Displays the result of a calculation. The `for` attribute is a space-separated list of the `id`s of the inputs that contribute to the output — declares the relationship semantically. Updated via JavaScript or the `oninput` event. Announced by screen readers as a live result.

## Key Points / Notes

- `<datalist>` suggestions are non-binding — the user can type anything, even if it's not in the list. For strictly constrained choices, use `<select>` instead.
- `<progress>` vs `<meter>`: progress is for **tasks** (how much is done). Meter is for **measurements** (how full, how strong, how much). Don't use them interchangeably — they have different semantics and different browser rendering.
- `<meter>` colors are determined by the browser based on how `value` relates to `low`, `high`, and `optimum`. You can't directly style the fill color in CSS across all browsers — it's one of the few elements with very limited styling support.
- The `for` attribute on `<output>` works similarly to `<label for>` — it declares which inputs the output is calculated from. Screen readers announce this relationship.
- `<progress>` and `<meter>` both have text content as fallback for older browsers — make it meaningful (e.g., "65%" or "7.5 GB of 10 GB used").
