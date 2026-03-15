```html
<!-- Images: always provide alt text -->
<img src="chart.png" alt="Bar chart showing 40% increase in sales from Q1 to Q4 2024" />
<img src="divider.png" alt="" />  <!-- decorative: empty alt -->

<!-- Forms: always connect labels to inputs -->
<label for="email">Email address</label>
<input type="email" id="email" name="email" required
       aria-describedby="email-hint" />
<p id="email-hint">We'll only use this to send your receipt.</p>

<!-- Links: descriptive text, not "click here" -->
<!-- Bad -->
<a href="/report.pdf">Click here</a>

<!-- Good -->
<a href="/report.pdf">Download the 2025 annual report (PDF, 2MB)</a>

<!-- Buttons vs links: use the right one -->
<!-- Link: navigates to a new page/location -->
<a href="/checkout">Go to Checkout</a>

<!-- Button: performs an action, no navigation -->
<button type="button" onclick="addToCart()">Add to Cart</button>

<!-- Heading hierarchy: correct order -->
<!-- Bad: skipping from h1 to h4 -->
<!-- <h1>Title</h1><h4>Subtitle</h4> -->

<!-- Good: logical nesting -->
<h1>Web Development</h1>
  <h2>Frontend</h2>
    <h3>HTML</h3>
    <h3>CSS</h3>
  <h2>Backend</h2>
    <h3>Go</h3>

<!-- Tables: always have headers with scope -->
<table>
  <caption>Course schedule</caption>
  <thead>
    <tr>
      <th scope="col">Day</th>
      <th scope="col">Topic</th>
      <th scope="col">Duration</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">Monday</th>
      <td>HTML Basics</td>
      <td>2 hours</td>
    </tr>
  </tbody>
</table>

<!-- Language declaration -->
<html lang="en">
<!-- Inline language switch -->
<p>The French word for hello is <span lang="fr">bonjour</span>.</p>
```

# Explanation

Semantic accessibility means using the correct, meaningful HTML element for each piece of content — so that the meaning is conveyed not just visually, but programmatically to every user, regardless of how they access the page.

## Breakdown

- **Alt text for images**  
  Describe what the image *communicates*, not its visual appearance. For a chart: describe the key insight ("40% increase"), not "a bar chart." For decorative images: `alt=""` (empty string) — screen readers skip it entirely.

- **Labels for form controls**  
  Every input must have an associated `<label>`. The `for` attribute on the label matches the `id` on the input. This is not optional — screen readers announce the label when a user focuses the input. `aria-describedby` adds supplementary hint text.

- **Descriptive link text**  
  Link text is read in isolation by screen readers ("Click here" tells them nothing). Describe the destination or action: "Download the 2025 annual report." If the destination needs clarification, add `aria-label`.

- **Buttons vs links**  
  `<a href>` navigates — it changes the URL. `<button>` performs an action in place — it doesn't change the URL. Using a `<button>` for navigation or an `<a>` for an action breaks the expected keyboard behaviour and confuses assistive technology.

- **Heading hierarchy**  
  Don't skip heading levels for visual effect. Screen reader users rely on headings for navigation — jumping from `<h1>` to `<h4>` creates a broken outline that implies missing sections. Use CSS to adjust visual size.

- **Table headers with `scope`**  
  `scope="col"` tells screen readers the header applies to everything in its column. `scope="row"` applies to everything in its row. Without `scope`, complex tables become incomprehensible when navigated cell-by-cell.

- **`<caption>` on tables**  
  Provides a title for the table — the first thing a screen reader announces. Without it, users hear "table, 3 columns, 5 rows" with zero context.

- **`lang` attribute**  
  Declared on `<html>` to set the page language. Screen readers use this to select the correct voice and pronunciation rules. For inline content in a different language (`<span lang="fr">`), the reader switches accent/voice for that portion.

## Key Points / Notes

- Accessible HTML is not a separate concern from "regular" HTML — it is just correct HTML. The same practices improve SEO, maintainability, and usability for all users.
- Screen readers read in source order. If you reorder elements visually with CSS (`order`, `flex-direction: row-reverse`), keyboard users and screen reader users still experience the original DOM order.
- "Good enough" accessibility is not enough. WCAG 2.1 Level AA is the legal standard in many countries. Level AA requires captions for video, sufficient color contrast, keyboard navigability, and proper labels.
- Colour alone must never be the only way to convey meaning (e.g., red = error). Always supplement with text, icons, or patterns — 8% of men have colour blindness.
- Automated accessibility checkers (axe DevTools, Lighthouse) are excellent but only catch ~30–40% of issues. Manual testing with a keyboard and screen reader is irreplaceable.
