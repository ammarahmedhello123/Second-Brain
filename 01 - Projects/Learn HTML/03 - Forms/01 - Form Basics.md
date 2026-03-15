```html
<!-- Basic form sending POST data to a server -->
<form action="/submit" method="POST">

  <label for="username">Username</label>
  <input type="text" id="username" name="username" required />

  <label for="email">Email</label>
  <input type="email" id="email" name="email" required />

  <label for="message">Message</label>
  <textarea id="message" name="message" rows="5"></textarea>

  <button type="submit">Send</button>

</form>

<!-- Search form — GET method (data in URL) -->
<form action="/search" method="GET" role="search">
  <label for="q">Search</label>
  <input type="search" id="q" name="q" placeholder="Search articles..." />
  <button type="submit">Go</button>
</form>

<!-- Fieldset groups related inputs -->
<form action="/register" method="POST">
  <fieldset>
    <legend>Personal Information</legend>
    <label for="fname">First Name</label>
    <input type="text" id="fname" name="first_name" />
    <label for="lname">Last Name</label>
    <input type="text" id="lname" name="last_name" />
  </fieldset>

  <fieldset>
    <legend>Account Details</legend>
    <label for="reg-email">Email</label>
    <input type="email" id="reg-email" name="email" />
    <label for="reg-pass">Password</label>
    <input type="password" id="reg-pass" name="password" />
  </fieldset>

  <button type="submit">Create Account</button>
</form>
```

# Explanation

The `<form>` element is the container for all form controls. When submitted, the browser collects all named controls inside it and sends the data to the server at the specified `action` URL using the specified `method`.

## Breakdown

- **`action`**  
  The URL the form data is submitted to. If omitted, the form submits to the current page's URL. Common targets are server-side endpoints like `/submit`, `/login`, or `/api/contact`.

- **`method="POST"`**  
  Sends form data in the HTTP request body — not visible in the URL. Use for any data that creates or modifies server state, contains sensitive info (passwords), or is large.

- **`method="GET"`**  
  Appends form data to the URL as a query string (`/search?q=html`). Use for search forms and filters — the resulting URL is shareable and bookmarkable. Never use GET for sensitive data.

- **`<label for="id">`**  
  Associates a text label with a control using matching `for` and `id` values. Clicking the label focuses the input. **Essential for accessibility** — without it, screen readers can't tell users what a field is for.

- **`name` attribute on inputs**  
  The key used in the submitted data. `name="email"` submits as `email=...`. Controls without a `name` are excluded from form data entirely.

- **`<fieldset>`**  
  Groups related controls into a logical section. Browsers draw a border around it by default (removable with CSS). Critical for grouping radio buttons and checkboxes accessibly.

- **`<legend>`**  
  The caption for a `<fieldset>`. Screen readers announce it before reading each control in the group — "Personal Information: First Name input."

- **`role="search"`**  
  ARIA landmark role on a search `<form>`. Lets screen reader users jump directly to the search form. Standard search forms benefit from this.

## Key Points / Notes

- Every control that should submit data **must** have a `name` attribute — controls without `name` are invisible to the server.
- `for` on `<label>` must match `id` on the input — not `name`. Many developers confuse these two. They are different attributes.
- Use `method="POST"` for login, registration, and any form that changes data. `method="GET"` for search, filter, and query forms.
- A `<form>` should never be nested inside another `<form>` — invalid HTML and undefined behaviour.
- Always validate form data on the **server side** in addition to client-side validation. Client-side can always be bypassed.
