```html
<!-- <template>: inert HTML fragment, not rendered until cloned -->
<template id="card-template">
  <div class="card">
    <img class="card__img" src="" alt="" />
    <div class="card__body">
      <h3 class="card__title"></h3>
      <p  class="card__desc"></p>
      <a  class="card__link" href="#">Read more</a>
    </div>
  </div>
</template>

<!-- Container where cloned cards will be injected -->
<div id="card-grid"></div>

<script>
  const data = [
    { title: "HTML Basics",     desc: "Learn the structure of the web.",    img: "html.jpg",  url: "/html"  },
    { title: "CSS Fundamentals",desc: "Style your pages beautifully.",       img: "css.jpg",   url: "/css"   },
    { title: "Go Language",     desc: "Fast, compiled, concurrent.",         img: "go.jpg",    url: "/go"    },
  ];

  const template = document.getElementById("card-template");
  const grid     = document.getElementById("card-grid");

  data.forEach(item => {
    // 1. Clone the template content
    const clone = template.content.cloneNode(true); // true = deep clone

    // 2. Fill in the placeholders
    clone.querySelector(".card__img").src         = item.img;
    clone.querySelector(".card__img").alt         = item.title;
    clone.querySelector(".card__title").textContent = item.title;
    clone.querySelector(".card__desc").textContent  = item.desc;
    clone.querySelector(".card__link").href         = item.url;

    // 3. Append to the DOM
    grid.appendChild(clone);
  });
</script>

<!-- Web Components: <slot> for composable custom elements -->
<script>
  class InfoCard extends HTMLElement {
    constructor() {
      super();
      const shadow = this.attachShadow({ mode: "open" });
      shadow.innerHTML = `
        <style>
          .card { border: 1px solid #1e2229; border-radius: 10px; padding: 16px; }
          ::slotted(h3) { color: #00add8; }
        </style>
        <div class="card">
          <slot name="title">Default Title</slot>
          <slot name="body">Default body content.</slot>
          <slot></slot>
        </div>
      `;
    }
  }
  customElements.define("info-card", InfoCard);
</script>

<!-- Using the custom element with named slots -->
<info-card>
  <h3 slot="title">My Custom Card</h3>
  <p  slot="body">This content goes into the named slot.</p>
  <span>This goes into the default (unnamed) slot.</span>
</info-card>
```

# Explanation

`<template>` holds reusable HTML fragments that are parsed but not rendered. Web Components use `<slot>` to define insertion points in a Shadow DOM, enabling truly encapsulated, reusable custom elements.

## Breakdown

- **`<template>`**  
  Contains inert HTML — parsed and validated by the browser, but not rendered, not in the document tree, and not accessible to queries. It's a staging area for markup you'll clone and use later. The content lives in `.content`, a `DocumentFragment`.

- **`template.content.cloneNode(true)`**  
  Clones the entire template content as a deep copy (including all child nodes). `true` = deep clone. Returns a `DocumentFragment`. Must be cloned — you can't append the same `.content` directly (it would move, not copy).

- **Filling in the clone**  
  Query within the cloned fragment with `.querySelector()` to find specific elements and set their properties before appending to the DOM. This is the key pattern: prepare in memory, then inject once.

- **`element.attachShadow({ mode: "open" })`**  
  Attaches a Shadow DOM to a custom element. `mode: "open"` means external JS can access it via `element.shadowRoot`. `"closed"` hides it. Shadow DOM provides true CSS and DOM encapsulation.

- **`<slot>`**  
  A placeholder inside a Shadow DOM template where the custom element's light DOM children are projected. Content passed between the custom element's tags ends up in the appropriate slot.

- **Named slot (`<slot name="title">`)**  
  A specific insertion point. Light DOM children with `slot="title"` are placed here. Allows structured composition — you define the layout, the consumer provides the content.

- **Default slot (`<slot>`)**  
  Catches all light DOM children that don't have a `slot` attribute. If no default slot exists, unmatched children are not rendered.

- **`::slotted(selector)`**  
  A Shadow DOM CSS pseudo-element that styles projected content from the light DOM. `::slotted(h3)` styles any `<h3>` slotted into the shadow.

## Key Points / Notes

- `<template>` is a performance pattern — parsing markup once and cloning it is significantly faster than building DOM nodes with `createElement` one by one, especially for large lists.
- The template content is not in the live DOM, so `document.querySelector()` won't find elements inside a `<template>`. Query from `template.content` instead.
- Web Components (`customElements.define`) work natively in all modern browsers with no framework or library needed. They produce real custom HTML elements that appear in DevTools like native elements.
- Shadow DOM CSS is scoped — styles inside the shadow don't leak out, and page styles don't leak in (except inherited properties like `color` and `font`). This solves the CSS global scope problem for component libraries.
- For large applications, frameworks like React, Vue, and Svelte provide component systems on top of these primitives — but understanding `<template>` and Web Components explains what they're abstracting.
