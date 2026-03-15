```html
<h1>Page Title — the main topic</h1>
<h2>Section Heading</h2>
<h3>Sub-section Heading</h3>
<h4>Sub-sub-section</h4>
<h5>Rarely used</h5>
<h6>Smallest heading</h6>
```

# Explanation

HTML provides six levels of headings — `<h1>` through `<h6>`. They define the document outline, a hierarchy that both users and search engines use to understand how the content is structured.

## Breakdown

- **`<h1>`**  
  The top-level heading. Describes the main topic of the entire page. There should be exactly **one** `<h1>` per page for clear SEO and document structure.

- **`<h2>`**  
  Major section headings. Think of them as chapter titles. Multiple `<h2>` elements per page are perfectly normal.

- **`<h3>`**  
  Sub-sections within an `<h2>` section. Useful for breaking a large section into focused parts.

- **`<h4>` – `<h6>`**  
  Increasingly deep subdivisions. `<h4>` is occasionally useful; `<h5>` and `<h6>` are rarely needed. If you find yourself needing them often, the content probably needs restructuring.

## Key Points / Notes

- Use headings in order (`h1 → h2 → h3`) without skipping levels. Jumping from `<h1>` to `<h4>` breaks the document outline.
- **Never** use headings just to make text larger or bolder — that's CSS's job. Tags should convey meaning, not appearance.
- Screen readers allow users to jump between headings to navigate the page. Correct heading hierarchy is essential for accessibility.
- `<h1>` carries the most SEO weight — make it descriptive and relevant to the page content.
- All browser default styles (size, weight) can be overridden with CSS. Choose tags based on semantics, not visual output.
