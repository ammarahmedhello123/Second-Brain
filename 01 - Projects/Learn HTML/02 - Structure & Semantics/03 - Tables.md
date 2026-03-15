```html
<table>
  <caption>Monthly Sales Report — Q1 2025</caption>

  <thead>
    <tr>
      <th scope="col">Product</th>
      <th scope="col">Units Sold</th>
      <th scope="col">Revenue</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>Widget A</td>
      <td>120</td>
      <td>$2,400</td>
    </tr>
    <tr>
      <td>Widget B</td>
      <td>85</td>
      <td>$1,700</td>
    </tr>
    <tr>
      <td>Widget C</td>
      <td>200</td>
      <td>$6,000</td>
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td>405</td>
      <td>$10,100</td>
    </tr>
  </tfoot>
</table>

<!-- Spanning cells -->
<table>
  <tr>
    <td colspan="2">Spans 2 columns →</td>
    <td>Normal</td>
  </tr>
  <tr>
    <td rowspan="2">Spans ↓ 2 rows</td>
    <td>Cell</td>
    <td>Cell</td>
  </tr>
  <tr>
    <td>Cell</td>
    <td>Cell</td>
  </tr>
</table>
```

# Explanation

Tables represent **tabular data** — information with a meaningful relationship between rows and columns, like a spreadsheet. The full structure with `<thead>`, `<tbody>`, and `<tfoot>` makes data comprehensible, printable, and accessible.

## Breakdown

- **`<table>`**  
  The container for the entire table. Takes only as much width as its content by default. All other table elements must be descendants of this.

- **`<caption>`**  
  A title placed immediately after the opening `<table>` tag. Rendered above the table and announced first by screen readers. The most accessible way to label a table — always include it.

- **`<thead>`**  
  Groups the header rows. The browser may repeat `<thead>` on each printed page in long tables. Visually and semantically separates column headings from data.

- **`<tbody>`**  
  The main data section. A table can have multiple `<tbody>` elements to group related rows (e.g., by category). Browsers add `<tbody>` implicitly if omitted, but explicitly including it is clearer.

- **`<tfoot>`**  
  Groups footer rows — typically totals, summaries, or notes. Always renders at the bottom regardless of where it appears in the source.

- **`<tr>` (Table Row)**  
  A single horizontal row containing `<th>` or `<td>` cells.

- **`<th>` (Table Header cell)**  
  A header cell — bold and centered by default. The `scope` attribute is critical for accessibility:  
  - `scope="col"` — this header describes its column.  
  - `scope="row"` — this header describes its row.

- **`<td>` (Table Data cell)**  
  A standard data cell. Left-aligned by default.

- **`colspan`**  
  Extends a cell across multiple columns. `colspan="2"` makes one cell occupy two column positions.

- **`rowspan`**  
  Extends a cell across multiple rows. `rowspan="2"` makes one cell occupy two row positions.

## Key Points / Notes

- **Tables are for tabular data only.** Never use `<table>` for page layout — that was a 1990s technique replaced by CSS Grid and Flexbox.
- Always use `<th scope="col">` for column headers and `<th scope="row">` for row headers. Screen reader users navigate tables cell by cell and rely on `scope` to know which header applies.
- `<caption>` is the table's accessible label. Without it, screen readers announce "table" with no context.
- For responsive tables on small screens, wrap the `<table>` in a `<div style="overflow-x: auto">` to allow horizontal scrolling.
- The `<colgroup>` and `<col>` elements can apply styles (like `width`) to entire columns without repeating attributes on every cell.
