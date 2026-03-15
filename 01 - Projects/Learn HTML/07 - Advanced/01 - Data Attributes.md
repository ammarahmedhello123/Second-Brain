```html
<!-- Storing data on elements with data-* attributes -->
<button
  data-user-id="42"
  data-action="delete"
  data-confirm="Are you sure?"
  onclick="handleAction(this)"
>
  Delete User
</button>

<!-- Data on list items -->
<ul id="product-list">
  <li data-product-id="101" data-price="29.99" data-category="electronics">
    Wireless Earbuds
  </li>
  <li data-product-id="102" data-price="49.99" data-category="electronics">
    Bluetooth Speaker
  </li>
</ul>

<!-- Reading data attributes in JavaScript -->
<script>
  function handleAction(button) {
    // Access via dataset property (camelCase conversion)
    const userId  = button.dataset.userId;   // "42"
    const action  = button.dataset.action;   // "delete"
    const confirm = button.dataset.confirm;  // "Are you sure?"

    if (window.confirm(confirm)) {
      console.log(`${action} user ${userId}`);
    }
  }

  // Query elements by data attribute
  const items = document.querySelectorAll("[data-category='electronics']");
  items.forEach(item => {
    const price = parseFloat(item.dataset.price);
    console.log(item.textContent, "-", price);
  });

  // Setting a data attribute via JS
  const btn = document.querySelector("button");
  btn.dataset.action = "restore"; // becomes data-action="restore" in HTML
</script>

<!-- Using data attributes for CSS styling -->
<style>
  [data-status="active"]   { color: green; }
  [data-status="inactive"] { color: gray;  }
  [data-status="banned"]   { color: red;   }
</style>

<span data-status="active">Active User</span>
<span data-status="banned">Banned User</span>
```

# Explanation

`data-*` attributes let you embed custom data directly on HTML elements. They are the clean, standards-compliant way to attach arbitrary metadata to elements for use by JavaScript and CSS — without polluting the element with non-standard attributes or hiding data in class names.

## Breakdown

- **`data-name="value"`**  
  Any attribute starting with `data-` is a custom data attribute. The name after `data-` can be anything you choose (lowercase, hyphens allowed). The value is always a string.

- **Naming convention**  
  Attribute names use lowercase and hyphens: `data-user-id`, `data-product-price`, `data-max-count`. No uppercase, no underscores in the HTML attribute name.

- **`element.dataset`**  
  JavaScript's API for reading and writing data attributes. The attribute name is converted to **camelCase** automatically: `data-user-id` → `dataset.userId`, `data-product-price` → `dataset.productPrice`.

- **Reading values**  
  `element.dataset.key` returns the value as a **string** — always. Parse numbers with `parseInt()` or `parseFloat()` when needed.

- **Writing values**  
  Setting `element.dataset.status = "active"` adds or updates `data-status="active"` on the element in the DOM.

- **Deleting values**  
  `delete element.dataset.key` removes the attribute from the element.

- **CSS attribute selectors**  
  CSS can select elements by their data attributes: `[data-status="active"]`. This is a clean way to drive visual state from a single source of truth in the HTML, without adding/removing class names.

- **`querySelectorAll("[data-category='electronics']")`**  
  Selects all elements with a specific data attribute value. A powerful, semantic alternative to class-based selection when querying by data rather than presentation.

## Key Points / Notes

- `data-*` values are always strings. Never store sensitive data (tokens, passwords) in data attributes — they're visible to anyone viewing the source or using DevTools.
- The naming rule: **HTML attribute** → lowercase, hyphens. **JavaScript `dataset`** → camelCase. `data-max-width` → `dataset.maxWidth`. The browser handles this conversion automatically.
- Don't overuse data attributes as a substitute for a proper data model. For complex state, store data in a JavaScript object and use the data attribute only as a reference key (like a foreign key).
- `data-*` attributes are searchable, queriable, and stylable — they're better than encoding info in class names like `class="product-42 category-electronics"`.
- The size of data stored in `data-*` attributes contributes to HTML file size. For large datasets, fetch via an API instead.
