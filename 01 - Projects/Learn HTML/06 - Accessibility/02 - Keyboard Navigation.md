```html
<!-- Skip link — lets keyboard users jump past navigation -->
<body>
  <a href="#main-content" class="skip-link">Skip to main content</a>

  <header>
    <nav><!-- long navigation --></nav>
  </header>

  <main id="main-content">
    <h1>Page Content</h1>
  </main>
</body>

<!-- tabindex values -->
<button>Naturally focusable (tabindex not needed)</button>
<a href="/page">Links are naturally focusable</a>

<!-- tabindex="0" — adds non-interactive element to natural tab order -->
<div role="button" tabindex="0" onclick="handleClick()" onkeydown="handleKey(event)">
  Custom button
</div>

<!-- tabindex="-1" — focusable via JS only, not Tab key -->
<div id="modal" tabindex="-1" role="dialog" aria-modal="true" aria-labelledby="modal-title">
  <h2 id="modal-title">Confirm Delete</h2>
  <p>Are you sure?</p>
  <button>Yes, Delete</button>
  <button>Cancel</button>
</div>

<!-- tabindex with positive value — explicit order (avoid this) -->
<!-- tabindex="1" tabindex="2" — creates confusion, avoid entirely -->

<!-- Focus management for modal -->
<script>
function openModal() {
  const modal = document.getElementById("modal");
  modal.removeAttribute("hidden");
  modal.focus(); // move focus into the modal
}

function handleKey(event) {
  // Custom keyboard widget must handle keyboard manually
  if (event.key === "Enter" || event.key === " ") {
    event.preventDefault();
    handleClick();
  }
}
</script>

<!-- Focus visible style (don't remove!) -->
<style>
  /* Never do this: */
  /* :focus { outline: none; } */

  /* Do this instead — custom visible focus style: */
  :focus-visible {
    outline: 2px solid #00ADD8;
    outline-offset: 3px;
    border-radius: 3px;
  }
</style>
```

# Explanation

Keyboard navigation is the primary mode of interaction for users with motor disabilities, power users, and anyone not using a mouse. Every interactive element on a page must be reachable and operable using only the keyboard.

## Breakdown

- **Skip link**  
  A link that is visually hidden but becomes visible on focus (via CSS). Allows keyboard users to bypass repetitive navigation and jump straight to the main content. Must be the very first focusable element in the `<body>`.

- **Natural focus order**  
  Interactive elements — `<a href>`, `<button>`, `<input>`, `<select>`, `<textarea>` — are automatically in the tab order based on their position in the DOM. No extra work needed.

- **`tabindex="0"`**  
  Makes a non-interactive element (like a custom `<div>` widget) part of the natural tab order. The element becomes focusable at its position in the DOM. Always pair with a `role` and keyboard event handlers.

- **`tabindex="-1"`**  
  Removes an element from the Tab key order but allows it to be focused programmatically with `.focus()` in JavaScript. Used for modals, drawers, and custom widgets where you manage focus manually.

- **Positive `tabindex`**  
  Values like `tabindex="1"`, `tabindex="2"` set an explicit order — but these jump to the front of the tab queue before any `tabindex="0"` elements. They almost always create confusing, unpredictable navigation. **Avoid entirely.**

- **Focus management for modals**  
  When a modal opens, move focus into it with `.focus()`. When it closes, return focus to the trigger element. Trap focus inside the modal so Tab cycles through only the modal's focusable elements.

- **`onkeydown` for custom widgets**  
  A `<div role="button" tabindex="0">` needs manual keyboard support. At minimum, handle `Enter` and `Space` to activate. Arrow keys for list/grid navigation. `Escape` to dismiss.

- **`:focus-visible`**  
  Shows a focus outline only when the element was focused via keyboard (not mouse click). Allows you to create a clean design for mouse users while still showing a clear focus indicator for keyboard users. Never use `:focus { outline: none }` without providing an alternative — it makes the page unusable for keyboard users.

## Key Points / Notes

- The most common keyboard accessibility mistake: removing focus styles with `outline: none` to avoid "ugly" default outlines. Instead, style `:focus-visible` with your own design.
- Logical DOM order = good keyboard order. Don't use CSS to reorder elements visually in a way that doesn't match the source order — Tab key follows the DOM, not the visual layout.
- Modal dialogs must trap focus — the Tab key should cycle through only the modal's interactive elements, not the background page. This requires JavaScript.
- Every custom interactive widget (carousel, accordion, tab panel, combobox) has an established keyboard interaction pattern in the ARIA Authoring Practices Guide (APG). Follow the pattern for that widget.
- Test by unplugging your mouse and navigating the entire page with only Tab, Shift+Tab, Enter, Space, and arrow keys. If anything is unreachable or unactivatable, it's a bug.
