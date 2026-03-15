```html
<!-- Landmark roles — help screen readers navigate the page -->
<div role="banner">Site header content</div>
<div role="navigation" aria-label="Main menu">...</div>
<div role="main">Primary page content</div>
<div role="complementary">Sidebar content</div>
<div role="contentinfo">Footer content</div>
<div role="search">
  <input type="text" aria-label="Search the site" />
  <button type="submit">Go</button>
</div>

<!-- aria-label — provides an accessible name where visible text is absent -->
<button aria-label="Close dialog">✕</button>
<a href="/cart" aria-label="Shopping cart, 3 items">🛒</a>
<nav aria-label="Breadcrumb">...</nav>

<!-- aria-labelledby — points to another element as the label -->
<h2 id="settings-title">Account Settings</h2>
<section aria-labelledby="settings-title">
  <p>Manage your account preferences here.</p>
</section>

<!-- aria-describedby — points to supplementary description -->
<label for="password">Password</label>
<input type="password" id="password" aria-describedby="pw-hint" />
<p id="pw-hint">Must be at least 8 characters and include a number.</p>

<!-- aria-hidden — removes element from accessibility tree -->
<span aria-hidden="true">👋</span> Hello!

<!-- aria-expanded — for toggles (menus, accordions) -->
<button aria-expanded="false" aria-controls="menu">Menu</button>
<ul id="menu" hidden>
  <li><a href="/">Home</a></li>
</ul>

<!-- aria-current — marks the active item -->
<nav>
  <a href="/" aria-current="page">Home</a>
  <a href="/about">About</a>
</nav>

<!-- aria-live — announces dynamic content to screen readers -->
<div aria-live="polite" aria-atomic="true" id="status"></div>
<div role="alert">Error: Please fix the highlighted fields.</div>

<!-- aria-required and aria-invalid on custom controls -->
<div role="textbox" contenteditable="true"
     aria-required="true"
     aria-invalid="false"
     aria-label="Full name">
</div>
```

# Explanation

ARIA (Accessible Rich Internet Applications) is a set of HTML attributes that communicate semantic meaning to assistive technologies when native HTML semantics are insufficient. The first rule of ARIA: **use native HTML elements first** — ARIA should supplement, not replace.

## Breakdown

- **`role`**  
  Overrides or assigns the ARIA role of an element. Native HTML elements already have implicit roles (`<button>` = `role="button"`, `<nav>` = `role="navigation"`). Use explicit `role` only when building custom widgets with non-semantic elements (`<div>`, `<span>`).

- **`aria-label`**  
  Provides a text name for an element when no visible label exists. Common uses: icon-only buttons, multiple navs on a page, inputs with no visible label.

- **`aria-labelledby`**  
  Points to the `id` of another element whose text serves as the label. Stronger than `aria-label` because the label is visible to sighted users too. Multiple IDs can be space-separated to concatenate labels.

- **`aria-describedby`**  
  Points to the `id` of supplementary descriptive text. Read after the label and role — "Password, edit, Must be at least 8 characters." Used for hints, error messages, and format instructions.

- **`aria-hidden="true"`**  
  Removes an element and all its children from the accessibility tree. Use for decorative icons, repeated elements, and visual content that would confuse screen readers if read aloud.

- **`aria-expanded`**  
  Indicates whether a collapsible widget (menu, accordion, dropdown) is currently open (`"true"`) or closed (`"false"`). Must be updated via JavaScript when the state changes.

- **`aria-controls`**  
  Points to the `id` of the element that a control manages. Pairs with `aria-expanded` on toggle buttons.

- **`aria-current`**  
  Marks the currently active item in a set — `"page"` for navigation links, `"step"` for progress steps, `"date"` for calendar dates.

- **`aria-live`**  
  Marks a region whose content updates dynamically. Screen readers will announce changes. `"polite"` waits until the user is idle. `"assertive"` interrupts immediately (use only for critical errors). `"off"` disables announcements.

- **`role="alert"`**  
  A live region with an implicit `aria-live="assertive"`. Immediately announced when content is injected. Use for error messages and critical status updates.

- **`aria-required` / `aria-invalid`**  
  For custom form controls not using native `<input>` — communicates required and validation state to screen readers. Use native `required` and validation attributes on actual `<input>` elements instead.

## Key Points / Notes

- **First rule of ARIA**: if a native HTML element exists that communicates the semantics you need, use it. `<button>` over `<div role="button">`. `<nav>` over `<div role="navigation">`.
- Adding a `role` gives an element semantics — but it doesn't add behaviour. A `<div role="button">` still needs `tabindex="0"` for keyboard focus and `onkeydown` handlers for Enter/Space. Native `<button>` handles all of that automatically.
- `aria-label` and `aria-labelledby` override the accessible name entirely — they don't append to it. If an element has both, `aria-labelledby` takes precedence.
- `aria-hidden="true"` does not visually hide an element — use CSS for that. It only hides from screen readers.
- Test with a real screen reader (NVDA on Windows, VoiceOver on Mac/iOS, TalkBack on Android) — automated tools catch only ~30–40% of accessibility issues.
