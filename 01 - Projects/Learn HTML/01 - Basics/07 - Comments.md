```html
<!-- This is a single-line comment — not rendered in the browser -->

<!-- Multi-line comment:
     Useful for longer explanations
     or temporarily disabling a block of code
-->

<!-- =============================================
     NAVIGATION SECTION
     ============================================= -->
<nav>
  <ul>
    <li><a href="/">Home</a></li>
  </ul>
</nav>

<!-- TODO: Add dropdown menu here -->
<!-- FIXME: Fix mobile layout on small screens -->

<!-- Temporarily disabling a section -->
<!--
<section class="beta-feature">
  <h2>Coming Soon</h2>
  <p>This feature is not ready yet.</p>
</section>
-->
```

# Explanation

HTML comments are notes left in the source code for developers. They are completely ignored by the browser and never rendered on the page. Anyone who views the page source can read them.

## Breakdown

- **`<!-- comment -->`**  
  The comment syntax. Starts with `<!--` and ends with `-->`. Everything between is ignored by the browser — no HTML is parsed inside a comment.

- **Single-line comment**  
  A brief note on one line. Used for short labels, reminders, or quick annotations directly above the relevant element.

- **Multi-line comment**  
  The same syntax — the browser doesn't care about line breaks inside `<!-- -->`. Use freely for longer explanations.

- **Section divider**  
  Using comment banners to visually separate major sections (`<!-- === HEADER === -->`) makes large HTML files navigable without a code editor's file outline.

- **TODO / FIXME tags**  
  Convention borrowed from programming: `<!-- TODO: ... -->` marks unfinished work, `<!-- FIXME: ... -->` marks known bugs. Many code editors highlight these automatically.

- **Commented-out code**  
  Wrapping HTML in `<!-- -->` disables it without deleting it. Useful during development for quickly toggling sections. Remove before going to production.

## Key Points / Notes

- Comments are visible in the page source. **Never** put passwords, API keys, internal URLs, or sensitive implementation details inside comments.
- HTML does not support nested comments — `<!-- outer <!-- inner --> -->` is invalid and will break unexpectedly.
- Commented-out code bloats the file size and clutters the codebase. Use version control (Git) to preserve deleted code instead of commenting it out permanently.
- Comments have no performance overhead when the page is being rendered — they are stripped before the DOM is built.
- Conditional comments (`<!--[if IE]>`) were an older technique for targeting Internet Explorer. They are obsolete and no longer needed.
