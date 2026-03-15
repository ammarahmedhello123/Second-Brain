```html
<head>
  <!-- 1. Character encoding — always first -->
  <meta charset="UTF-8" />

  <!-- 2. Responsive viewport — always second -->
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <!-- 3. Page description (shown in search results) -->
  <meta name="description" content="Learn HTML from scratch with clear examples and beginner-friendly explanations." />

  <!-- 4. Author -->
  <meta name="author" content="Ammar Ahmed" />

  <!-- 5. Robots — control search engine crawling -->
  <meta name="robots" content="index, follow" />

  <!-- 6. Page title -->
  <title>HTML Basics — Learn HTML</title>

  <!-- 7. Theme color — browser chrome color on mobile -->
  <meta name="theme-color" content="#0d0f12" />

  <!-- 8. Open Graph — social media sharing previews -->
  <meta property="og:title"       content="HTML Basics — Learn HTML" />
  <meta property="og:description" content="Learn HTML from scratch." />
  <meta property="og:image"       content="https://example.com/og-cover.jpg" />
  <meta property="og:url"         content="https://example.com/html-basics" />
  <meta property="og:type"        content="article" />
  <meta property="og:site_name"   content="Learn HTML" />

  <!-- 9. Twitter Card -->
  <meta name="twitter:card"        content="summary_large_image" />
  <meta name="twitter:title"       content="HTML Basics — Learn HTML" />
  <meta name="twitter:description" content="Learn HTML from scratch." />
  <meta name="twitter:image"       content="https://example.com/og-cover.jpg" />

  <!-- 10. Canonical URL — prevents duplicate content -->
  <link rel="canonical" href="https://example.com/html-basics" />

</head>
```

# Explanation

`<meta>` tags provide structured information *about* the page to browsers, search engines, and social platforms. None of it is rendered on the page — it all works behind the scenes to control how the page is found, displayed, and shared.

## Breakdown

- **`charset="UTF-8"`**  
  Always the very first tag in `<head>`. Sets character encoding before the browser parses anything else. Supports all languages, scripts, and emoji.

- **`name="viewport"`**  
  Prevents mobile browsers from scaling the page down to fit the screen. `width=device-width` makes the page width match the device. `initial-scale=1.0` prevents automatic zoom. Without this, your responsive CSS does nothing on mobile.

- **`name="description"`**  
  A 150–160 character summary of the page. Shown as the snippet text in Google search results. Doesn't directly affect ranking but heavily influences click-through rate. Write it like an ad for the page.

- **`name="author"`**  
  The page author's name. Used by some browsers and parsers. Low SEO impact but good practice for documentation.

- **`name="robots"`**  
  Instructions for crawlers. `index` = include in search results. `noindex` = exclude. `follow` = crawl links on this page. `nofollow` = don't. Use `noindex, nofollow` on admin pages, staging environments, and private content.

- **`<title>`**  
  Not a `<meta>` tag technically, but the most important `<head>` element. Shown in the browser tab, bookmarks, and as the blue headline in Google results. Keep under 60 characters and front-load the important keywords.

- **`name="theme-color"`**  
  Colors the browser's address bar and status bar on mobile Chrome and some other browsers. Good for PWA (Progressive Web App) branding.

- **`property="og:*"` — Open Graph**  
  Controls how the page looks when shared on Facebook, LinkedIn, Slack, WhatsApp, and most social platforms. `og:image` is the preview thumbnail (recommend 1200×630px). Without OG tags, platforms scrape a random image and use the page title.

- **`name="twitter:card"`**  
  Twitter-specific metadata (still works on X). `"summary_large_image"` shows a wide banner image. `"summary"` shows a small thumbnail beside the text.

- **`rel="canonical"`**  
  Tells search engines which URL is the single "official" version of this content. Prevents duplicate content penalties when the same content is accessible at multiple URLs (with/without trailing slash, with UTM parameters, HTTPS vs HTTP).

## Key Points / Notes

- The order in `<head>` matters. `charset` first, `viewport` second — these must be parsed early for correct rendering.
- `name="keywords"` was used in the 1990s. Google has ignored it since ~2009. Still valid HTML, but functionally useless for SEO.
- `og:image` is the highest-impact thing you can add for social sharing. A compelling image dramatically increases engagement on shared links.
- Every page on a site should have a **unique** `<title>` and `<meta name="description">`. Duplicate titles and descriptions hurt SEO.
- `rel="canonical"` should be self-referencing on every page, even if there's no obvious duplication risk. It's a defensive best practice.
