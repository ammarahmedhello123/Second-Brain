```html
<!-- Default enctype — for all forms without file uploads -->
<form action="/submit" method="POST" enctype="application/x-www-form-urlencoded">
  <label for="name">Name</label>
  <input type="text" id="name" name="name" value="Ammar" />

  <label for="email">Email</label>
  <input type="email" id="email" name="email" value="ammar@example.com" />

  <button type="submit">Submit</button>
</form>
<!-- Submitted as: name=Ammar&email=ammar%40example.com -->

<!-- ─────────────────────────────────────────── -->

<!-- multipart/form-data — REQUIRED for file uploads -->
<form action="/upload" method="POST" enctype="multipart/form-data">
  <label for="avatar">Profile Photo</label>
  <input type="file" id="avatar" name="avatar" accept="image/*" />

  <label for="username">Username</label>
  <input type="text" id="username" name="username" />

  <button type="submit">Upload</button>
</form>

<!-- Multiple file upload -->
<form action="/upload-docs" method="POST" enctype="multipart/form-data">
  <label for="docs">Documents (PDF)</label>
  <input type="file" id="docs" name="docs" accept=".pdf" multiple />
  <button type="submit">Upload All</button>
</form>

<!-- ─────────────────────────────────────────── -->

<!-- text/plain — human-readable, rarely used (no encoding) -->
<form action="mailto:hello@example.com" method="POST" enctype="text/plain">
  <label for="msg">Message</label>
  <textarea id="msg" name="msg"></textarea>
  <button type="submit">Send via Email</button>
</form>
<!-- Output: name=value pairs with \r\n, no URL encoding — unreliable for data -->

<!-- ─────────────────────────────────────────── -->

<!-- Submitting files via JavaScript Fetch with FormData -->
<form id="upload-form">
  <input type="file" name="photo" accept="image/*" />
  <input type="text" name="caption" placeholder="Caption" />
  <button type="button" onclick="submitForm()">Upload</button>
</form>

<script>
  function submitForm() {
    const form = document.getElementById("upload-form");
    const formData = new FormData(form); // automatically sets multipart/form-data

    fetch("/api/upload", {
      method: "POST",
      body: formData
      // DO NOT set Content-Type header manually — browser sets it with the correct boundary
    })
    .then(res => res.json())
    .then(data => console.log(data));
  }
</script>
```

# Explanation

`enctype` (encoding type) on a `<form>` controls how the form data is encoded when it is sent to the server. The default encoding works for text data. For file uploads, you **must** use `multipart/form-data` — without it, only the filename is sent, not the file contents.

## Breakdown

- **`application/x-www-form-urlencoded`** (default)  
  All form data is encoded as a URL query string: `key=value&key2=value2`. Special characters are percent-encoded (spaces become `+` or `%20`, `@` becomes `%40`). The entire submission is a single flat string. Works perfectly for text-only forms. This is the default — you don't need to write it explicitly.

- **`multipart/form-data`**  
  The form data is split into separate "parts," each with its own headers, separated by a randomly generated `boundary` string. Each file is sent as its own part with the full binary content included. **Required for any form that includes `<input type="file">`**. Without it, only the filename string is transmitted — the actual file bytes are never sent.

- **`text/plain`**  
  Data sent as plain text with line breaks between key-value pairs. No encoding — special characters are not escaped. Intended for human-readable email submissions (`action="mailto:..."`). Unreliable for machine processing and essentially never used in modern web apps.

- **Boundary string**  
  In `multipart/form-data`, the browser automatically generates a unique boundary string (e.g., `----WebKitFormBoundary7MA4YWxkTrZu0gW`) and includes it in the `Content-Type` header. Each form field and file is separated by this boundary in the request body. This is handled entirely by the browser — you never need to set it manually.

- **`FormData` API (JavaScript)**  
  `new FormData(formElement)` creates a FormData object from a form. When passed to `fetch()` as the `body`, it automatically uses `multipart/form-data` encoding with the correct boundary. **Never set `Content-Type` manually when using FormData** — the browser must set it itself to include the boundary string. Setting it manually will break the upload.

## Key Points / Notes

- Forgetting `enctype="multipart/form-data"` on file upload forms is one of the most common HTML mistakes. The form submits, the server receives the request, but `req.file` (or equivalent) is always `undefined`.
- `multipart/form-data` can also send regular text fields — they're just included as separate parts. You don't need separate forms for text + file data.
- The `method` must be `POST` for file uploads. `GET` encodes data in the URL — binary file data cannot be URL-encoded.
- Server-side handling: the server must use a multipart parser (like `multer` in Node.js, `multipart` in Go's `net/http`, or `request.FILES` in Django) to extract uploaded files from the multipart body.
- File size limits are enforced server-side (not in HTML). Set `max_file_size` in your server config and handle oversized uploads gracefully — HTML's `<input type="file">` has no built-in size limit attribute.
