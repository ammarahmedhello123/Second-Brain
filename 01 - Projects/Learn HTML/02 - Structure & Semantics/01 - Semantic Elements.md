```html
<body>

  <header>
    <a href="/" aria-label="Go to homepage">
      <img src="logo.svg" alt="Company Logo" />
    </a>
    <nav aria-label="Main navigation">
      <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/blog">Blog</a></li>
      </ul>
    </nav>
  </header>

  <main>

    <article>
      <header>
        <h1>How to Learn HTML</h1>
        <p>By <address>Ammar Ahmed</address> — <time datetime="2025-03-15">March 15, 2025</time></p>
      </header>

      <section>
        <h2>Getting Started</h2>
        <p>Begin with the document structure...</p>
      </section>

      <section>
        <h2>Core Concepts</h2>
        <p>Learn tags, attributes, and nesting...</p>
      </section>

      <footer>
        <p>Tags: <a href="/tag/html">HTML</a>, <a href="/tag/beginner">Beginner</a></p>
      </footer>
    </article>

    <aside>
      <h2>Related Articles</h2>
      <ul>
        <li><a href="/css-basics">CSS Basics</a></li>
        <li><a href="/js-intro">JavaScript Intro</a></li>
      </ul>
    </aside>

  </main>

  <footer>
    <p>&copy; 2025 My Site. <a href="/privacy">Privacy Policy</a></p>
  </footer>

</body>
```

# Explanation

Semantic HTML uses tags that describe the **role and meaning** of content — not just how it looks. This benefits accessibility tools, search engines, and other developers reading the code. A `<nav>` communicates "navigation" in a way a `<div class="nav">` never can.

## Breakdown

- **`<header>`**  
  Introductory content for its nearest sectioning ancestor. At the `<body>` level it's the site header (logo, nav). Inside `<article>` it holds the article's title, author, and date. Not the same as `<head>`.

- **`<nav>`**  
  A block of major navigation links. Use for the main site menu, a table of contents, or breadcrumbs. Screen readers expose it as a navigation landmark — users can jump to or skip it quickly.

- **`<main>`**  
  The primary, unique content of the page. Only **one** per page. Screen readers provide a "skip to main content" shortcut targeting this element — critical for keyboard users.

- **`<article>`**  
  A self-contained, independently distributable piece of content. Ask: "Would this make sense lifted out of context and placed elsewhere?" Blog posts, news articles, product cards, and forum posts are all good candidates.

- **`<section>`**  
  A thematic grouping within a larger document. Every `<section>` should have a heading. Use it when content forms a distinct part of a whole but wouldn't stand alone. If there's no heading, use a `<div>` instead.

- **`<aside>`**  
  Content tangentially related to the main content — a sidebar, related links, pull quote, or advertisement. Not part of the primary reading flow.

- **`<footer>`**  
  Closing content for its nearest sectioning ancestor. At page level: copyright, legal links. Inside `<article>`: tags, publication date, author info.

- **`<time datetime="...">`**  
  A specific point in time. The human-readable text is for display; the `datetime` attribute provides a machine-readable ISO 8601 value that browsers, search engines, and calendar apps can parse.

- **`<address>`**  
  Contact information for the nearest `<article>` or `<body>`. Not for postal addresses in general — specifically for the author or owner's contact details.

## Key Points / Notes

- `<div>` and `<span>` convey nothing to the browser or assistive tech. Every time you use a semantic element instead, you're communicating structure for free.
- The landmark elements (`<header>`, `<nav>`, `<main>`, `<aside>`, `<footer>`) form an accessibility map that screen reader users rely on to navigate.
- `<section>` is not a generic wrapper — if you're using it with no heading and only for layout, use `<div>` instead.
- `<article>` can contain `<section>`s. A `<section>` generally should not contain multiple unrelated `<article>`s.
- Search engines give greater weight to content inside `<article>` and `<main>`. Proper semantics have direct SEO benefits.
