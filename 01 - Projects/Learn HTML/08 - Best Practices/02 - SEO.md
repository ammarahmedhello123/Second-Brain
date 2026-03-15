```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- Title: unique, descriptive, keyword-first, under 60 chars -->
  <title>Learn HTML in 2025 — Complete Beginner Guide</title>

  <!-- Description: 150-160 chars, acts as your search result ad copy -->
  <meta name="description" content="Learn HTML from scratch with hands-on examples. Master tags, semantics, forms, and best practices in this complete 2025 guide." />

  <!-- Canonical: prevents duplicate content penalties -->
  <link rel="canonical" href="https://example.com/learn-html" />

  <!-- Open Graph for rich social previews -->
  <meta property="og:title"       content="Learn HTML in 2025 — Complete Guide" />
  <meta property="og:description" content="Master HTML with hands-on examples and clear explanations." />
  <meta property="og:image"       content="https://example.com/og/learn-html.jpg" />
  <meta property="og:url"         content="https://example.com/learn-html" />
  <meta property="og:type"        content="article" />

  <!-- Robots: control indexing -->
  <meta name="robots" content="index, follow" />

</head>
<body>

  <!-- One h1 per page, contains the primary keyword -->
  <h1>Learn HTML: A Complete Beginner's Guide for 2025</h1>

  <!-- Breadcrumb navigation (also helps SEO) -->
  <nav aria-label="Breadcrumb">
    <ol>
      <li><a href="/">Home</a></li>
      <li><a href="/tutorials">Tutorials</a></li>
      <li aria-current="page">Learn HTML</li>
    </ol>
  </nav>

  <article>
    <!-- Structured heading hierarchy -->
    <h2>What is HTML?</h2>
    <p>HTML stands for HyperText Markup Language...</p>

    <h2>Getting Started</h2>
    <h3>Step 1: Create Your First File</h3>
    <p>Open a text editor and create <code>index.html</code>...</p>

    <h3>Step 2: Add Basic Structure</h3>
    <p>Every HTML file starts with <code>&lt;!DOCTYPE html&gt;</code>...</p>

    <!-- Internal links help crawlers discover pages -->
    <p>Once you know HTML, learn <a href="/learn-css">CSS for styling</a> and
    <a href="/learn-js">JavaScript for interactivity</a>.</p>

    <!-- Publication date for freshness signals -->
    <footer>
      <time datetime="2025-03-15">Last updated: March 15, 2025</time>
    </footer>
  </article>

  <!-- Structured data (JSON-LD) — tells Google rich snippet info -->
  <script type="application/ld+json">
  {
    "@context": "https://schema.org",
    "@type": "Article",
    "headline": "Learn HTML: A Complete Beginner's Guide for 2025",
    "description": "Master HTML with hands-on examples.",
    "datePublished": "2025-01-01",
    "dateModified": "2025-03-15",
    "author": {
      "@type": "Person",
      "name": "Ammar Ahmed"
    }
  }
  </script>

</body>
</html>
```

# Explanation

SEO (Search Engine Optimization) at the HTML level is about communicating meaning clearly to search crawlers — through well-structured headings, descriptive metadata, semantic elements, and structured data. Good semantic HTML is good SEO.

## Breakdown

- **`<title>`**  
  The most important SEO element. Shown as the clickable headline in Google results. Keep it under 60 characters. Front-load the primary keyword. Make it unique per page.

- **`<meta name="description">`**  
  The snippet text shown in search results. Google often rewrites it, but providing a good one improves CTR (click-through rate). 150–160 characters. Treat it like ad copy — make it compelling and accurate.

- **`rel="canonical"`**  
  Prevents duplicate content issues. When the same content is accessible at multiple URLs (trailing slash, query params, HTTP vs HTTPS), the canonical URL tells Google which one to index. Self-reference on every page as a defensive measure.

- **Open Graph tags**  
  Improve how pages look when shared on social media. `og:image` (1200×630px recommended) is the most impactful tag — a good image dramatically increases engagement.

- **One `<h1>`**  
  One per page. Contains the primary keyword for the page. Every additional page section gets an `<h2>`, sub-sections get `<h3>`. Clear heading hierarchy = clear document structure for crawlers.

- **`<article>` for main content**  
  Search engines give extra semantic weight to content inside `<article>`. It signals "this is the primary content," not boilerplate navigation or footer.

- **Internal links with descriptive anchor text**  
  Link to related pages with descriptive text ("learn CSS for styling" not "click here"). This distributes PageRank across your site and helps crawlers understand page relationships.

- **`<time datetime>`**  
  Machine-readable publication and modification dates. Used by Google to determine content freshness — important for news and tutorial content.

- **JSON-LD structured data**  
  A `<script type="application/ld+json">` containing Schema.org markup. Tells Google rich details about the content — enabling rich snippets (star ratings, article dates, FAQ dropdowns) in search results.

- **Breadcrumb navigation**  
  An ordered list showing the page's position in the site hierarchy. Google displays breadcrumbs in search results instead of the full URL, improving click-through rates.

## Key Points / Notes

- `<meta name="keywords">` has been ignored by Google since ~2009. It still appears in templates but has zero SEO value.
- Page speed is a ranking factor. HTML-level performance improvements (lazy loading, preconnect, correct script loading) directly impact SEO.
- Google renders JavaScript, but server-side rendered (or static) HTML is indexed more reliably and faster. Critical content should be in the initial HTML, not injected by JS.
- Duplicate `<title>` and `<meta name="description">` across pages are a common SEO error. Every page must have unique values.
- The JSON-LD block can go in `<head>` or `<body>` — Google supports both. `<body>` before `</body>` is the conventional placement.
