```html
<!-- Reserved characters that must be escaped -->
<p>Use &lt;p&gt; tags for paragraphs.</p>       <!-- < > -->
<p>Type &amp; to write an ampersand.</p>         <!-- & -->
<p>She said &quot;hello&quot; to him.</p>        <!-- " -->
<p>It&apos;s a great day.</p>                    <!-- ' -->

<!-- Non-breaking space — prevents line wrap -->
<p>100&nbsp;km/h</p>
<p>Copyright&nbsp;&copy;&nbsp;2025</p>

<!-- Common symbols -->
<p>&copy; 2025 Company Name</p>   <!-- © -->
<p>&reg; Registered Trademark</p> <!-- ® -->
<p>&trade; Trademark Symbol</p>   <!-- ™ -->

<!-- Typography -->
<p>&mdash; em dash (sentence break)</p>    <!-- — -->
<p>&ndash; en dash (range: 10&ndash;20)</p> <!-- – -->
<p>&ldquo;Curly open quote&rdquo;</p>       <!-- " " -->
<p>&lsquo;Single open quote&rsquo;</p>      <!-- ' ' -->
<p>&hellip; ellipsis</p>                    <!-- … -->

<!-- Math and currency -->
<p>5 &times; 3 = 15</p>          <!-- × -->
<p>10 &divide; 2 = 5</p>         <!-- ÷ -->
<p>Price: &euro;9 or &pound;8</p> <!-- € £ -->
<p>100&deg;C</p>                  <!-- ° -->
<p>&frac12; &frac14; &frac34;</p> <!-- ½ ¼ ¾ -->

<!-- Numeric references (decimal and hex) -->
<p>&#169; = &#xA9; = &copy;</p>
```

# Explanation

HTML entities are escape codes that represent characters that either have special meaning in HTML syntax (like `<` and `&`) or aren't available on a standard keyboard. They always start with `&` and end with `;`.

## Breakdown

- **`&lt;` and `&gt;`**  
  Less-than (`<`) and greater-than (`>`). These are the tag delimiters in HTML — the parser treats them as the start and end of tags. To show them as literal text (like in code examples), they must be escaped.

- **`&amp;`**  
  The ampersand (`&`). Since `&` starts all entity codes, a literal ampersand in text must be written as `&amp;`. Especially important inside `href` attribute values containing query strings.

- **`&quot;` and `&apos;`**  
  Double quote (`"`) and apostrophe/single quote (`'`). Needed when those characters appear inside an attribute value that uses the same quote style.

- **`&nbsp;`**  
  Non-breaking space. Looks like a space but prevents a line wrap at that point. Also stops multiple spaces from collapsing into one (HTML collapses consecutive whitespace by default).

- **`&copy;` / `&reg;` / `&trade;`**  
  Copyright (©), registered trademark (®), trademark (™). Commonly used in page footers.

- **`&mdash;` and `&ndash;`**  
  Em dash (—) used for parenthetical breaks in sentences. En dash (–) used for numeric ranges (pages 10–20). Both are typographically distinct from a plain hyphen (-).

- **`&ldquo;` `&rdquo;` / `&lsquo;` `&rsquo;`**  
  Typographically correct "curly" (or "smart") quotes — the kind used in properly typeset books and print. Visually superior to straight ASCII quotes.

- **Numeric references**  
  Reference any Unicode character by its code point. Decimal (`&#N;`) or hexadecimal (`&#xN;`). `&#169;` and `&#xA9;` both produce ©. Useful for characters that have no named entity.

- **`&hellip;`**  
  The proper ellipsis character (…) — a single typographic glyph, not three separate period characters. Renders more consistently and line-wraps better.

## Key Points / Notes

- With `<meta charset="UTF-8">` you can type most special characters (©, é, →, 日) directly in your file. Entities are mainly required for the four reserved HTML characters: `<`, `>`, `&`, and `"`.
- **Security**: when inserting user-provided text into HTML, always escape `<`, `>`, `&`, `"`, and `'` to prevent XSS (Cross-Site Scripting) attacks. Frameworks usually handle this automatically.
- `&nbsp;` is misused for indentation and spacing all the time — use CSS `margin`, `padding`, and `letter-spacing` instead. Reserve `&nbsp;` for true non-breaking cases.
- Named entities (`&copy;`, `&mdash;`) are more readable in source than numeric equivalents — prefer them when available.
- HTML5 dropped some entity names from older HTML versions — always test obscure ones for browser support.
