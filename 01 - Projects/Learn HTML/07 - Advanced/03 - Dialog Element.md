```html
<!-- Native modal dialog -->
<dialog id="confirm-dialog" aria-labelledby="dialog-title">
  <h2 id="dialog-title">Confirm Delete</h2>
  <p>Are you sure you want to delete this item? This action cannot be undone.</p>
  <div class="dialog-actions">
    <button id="confirm-btn" autofocus>Yes, Delete</button>
    <button id="cancel-btn">Cancel</button>
  </div>
</dialog>

<!-- Trigger button -->
<button id="open-btn">Delete Item</button>

<script>
  const dialog    = document.getElementById("confirm-dialog");
  const openBtn   = document.getElementById("open-btn");
  const cancelBtn = document.getElementById("cancel-btn");
  const confirmBtn= document.getElementById("confirm-btn");

  // Open as a modal (traps focus, shows backdrop)
  openBtn.addEventListener("click", () => dialog.showModal());

  // Open as non-modal (no focus trap, no backdrop)
  // openBtn.addEventListener("click", () => dialog.show());

  // Close on cancel
  cancelBtn.addEventListener("click", () => dialog.close());

  // Close on confirm
  confirmBtn.addEventListener("click", () => {
    // perform delete action...
    dialog.close("confirmed"); // optional return value
  });

  // Close when clicking the backdrop (outside the dialog)
  dialog.addEventListener("click", (e) => {
    if (e.target === dialog) dialog.close();
  });

  // Listen for close event and read the return value
  dialog.addEventListener("close", () => {
    console.log("Dialog closed with:", dialog.returnValue);
  });
</script>

<!-- Dialog inside a form (form method dialog) -->
<dialog id="form-dialog">
  <form method="dialog">
    <h2>Settings</h2>
    <label for="theme-select">Theme</label>
    <select id="theme-select" name="theme">
      <option value="dark">Dark</option>
      <option value="light">Light</option>
    </select>
    <!-- submit closes the dialog and sets returnValue to the submit button's value -->
    <button type="submit" value="save">Save</button>
    <button type="submit" value="cancel">Cancel</button>
  </form>
</dialog>

<style>
  dialog {
    border: 1px solid #1e2229;
    border-radius: 10px;
    padding: 24px;
    background: #13161b;
    color: #dce3ee;
  }

  dialog::backdrop {
    background: rgba(0, 0, 0, 0.7);
    backdrop-filter: blur(4px);
  }
</style>
```

# Explanation

The native `<dialog>` element provides a built-in modal and non-modal dialog with automatic focus management, `Escape` key support, the `::backdrop` pseudo-element, and a simple JavaScript API. It replaces complex DIV-based modal implementations.

## Breakdown

- **`<dialog>`**  
  The container for dialog content. Hidden by default (via `display: none`). Becomes visible when opened via `.show()` or `.showModal()`.

- **`dialog.showModal()`**  
  Opens the dialog as a **modal**:  
  - Traps keyboard focus inside the dialog.  
  - `Escape` key closes it automatically.  
  - Renders the `::backdrop` overlay.  
  - Places the dialog in the top layer (above everything, including `z-index` stacking).

- **`dialog.show()`**  
  Opens the dialog as a **non-modal** (modeless) dialog. No focus trap, no backdrop, no Escape key binding. The rest of the page remains interactive.

- **`dialog.close(returnValue)`**  
  Closes the dialog. The optional `returnValue` string is stored in `dialog.returnValue` and can be read in the `close` event handler — useful for knowing which button the user pressed.

- **`autofocus`**  
  The element with `autofocus` inside the dialog receives focus when the dialog opens. Put it on the primary action button or the first input.

- **Closing on backdrop click**  
  The `<dialog>` element doesn't close on backdrop click by default (unlike many library modals). Implement it by listening for `click` events on the `<dialog>` itself and checking if `event.target === dialog`.

- **`form method="dialog"`**  
  A `<form>` with `method="dialog"` inside a `<dialog>` — when submitted, it closes the dialog and sets `dialog.returnValue` to the `value` of the submit button that was clicked. No server request is made.

- **`dialog::backdrop`**  
  A CSS pseudo-element that represents the backdrop overlay shown behind a modal dialog. Fully styleable with CSS — color, opacity, blur, etc.

- **`close` event**  
  Fired when the dialog is closed by any means (`.close()`, `Escape` key, form submit). Read `dialog.returnValue` here to handle the result.

## Key Points / Notes

- `<dialog>` handles focus trapping automatically in `showModal()` mode — no JavaScript library needed. This was previously the hardest part of building accessible modals.
- Always set `aria-labelledby` pointing to the dialog's heading, or `aria-label` if there's no visible heading. Screen readers announce this as the dialog's name when it opens.
- `Escape` key support is built into `showModal()`. Don't disable it — it's the expected keyboard affordance for dismissing a modal.
- The `::backdrop` exists in the top layer, separate from the normal stacking context. You can't accidentally put content over it with `z-index`. This is a major advantage over DIV-based modals.
- For animation, the `<dialog>` element supports CSS `@starting-style` for entry animations in modern browsers, and exit animations can be achieved by listening to the `close` event and adding an animation class before closing.
