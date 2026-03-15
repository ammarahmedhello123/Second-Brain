```html
<form action="/register" method="POST" novalidate>

  <!-- required — field must not be empty -->
  <label for="name">Full Name *</label>
  <input type="text" id="name" name="name" required />

  <!-- minlength / maxlength -->
  <label for="username">Username *</label>
  <input type="text" id="username" name="username"
         minlength="3" maxlength="20" required />

  <!-- min / max on number -->
  <label for="age">Age *</label>
  <input type="number" id="age" name="age" min="18" max="99" required />

  <!-- pattern — custom regex validation -->
  <label for="postcode">Postcode *</label>
  <input type="text" id="postcode" name="postcode"
         pattern="[0-9]{5}" title="Enter a 5-digit postcode" required />

  <!-- Email auto-validates format -->
  <label for="email">Email *</label>
  <input type="email" id="email" name="email" required />

  <!-- Password with pattern -->
  <label for="password">Password (min 8 chars, 1 number) *</label>
  <input type="password" id="password" name="password"
         pattern="^(?=.*[0-9]).{8,}$"
         title="At least 8 characters, including one number"
         required />

  <!-- Checkbox must be checked -->
  <input type="checkbox" id="terms" name="terms" value="agreed" required />
  <label for="terms">I agree to the Terms of Service *</label>

  <!-- novalidate on form — disables all native validation (for custom JS) -->
  <button type="submit">Register</button>

</form>
```

# Explanation

HTML5 includes built-in form validation that runs before the form is submitted. It's free, accessible, and works without JavaScript. Combine it with server-side validation for complete coverage.

## Breakdown

- **`required`**  
  A boolean attribute — the field must have a non-empty value before the form can submit. If empty on submit, the browser shows a tooltip and prevents submission.

- **`minlength` / `maxlength`**  
  Constrains the length of text input. `minlength` triggers a validation error if the input is too short. `maxlength` prevents typing beyond the limit (no error — the input simply stops accepting more characters).

- **`min` / `max`**  
  For `type="number"`, `type="range"`, and date/time inputs — constrains the allowed value range. Values outside this range fail validation.

- **`pattern`**  
  A regular expression that the value must fully match. Applied to text-like inputs (`text`, `tel`, `url`, `password`, `search`). The `title` attribute provides the error hint shown to the user.

- **`type="email"`**  
  Automatically validates that the value matches an email pattern (`text@domain.tld`). No `pattern` needed.

- **`step`**  
  On `type="number"` and `type="range"` — defines valid increments. `step="2"` means only even numbers are valid (relative to `min`). Non-step-aligned values fail validation.

- **`novalidate`**  
  A boolean attribute on `<form>` that disables all native HTML validation. Use when you're implementing full custom JavaScript validation and want full control over error messages and styling.

- **`:valid` and `:invalid` CSS pseudo-classes**  
  CSS can target form controls based on their validation state: `input:invalid { border-color: red; }`. Use `:user-invalid` (newer) to only show errors after the user has interacted with the field, avoiding showing errors on pristine/untouched fields.

## Key Points / Notes

- Native HTML validation is the first line of defence — fast, accessible, and zero JS. But it is **not** a replacement for server-side validation. Never trust the client.
- `pattern` uses JavaScript RegEx syntax but doesn't need the surrounding `/` slashes. The browser automatically anchors to the full string (`^...$`), so you don't need those either.
- The `title` attribute on a field with `pattern` is shown as the validation error message in most browsers — always write it in plain language.
- `required` on a `<select>` works if the empty option has `value=""` — the browser treats an empty value as "not selected."
- CSS `:invalid` fires immediately on page load for empty `required` fields. Use `:user-invalid` or add a `.touched` class via JavaScript to avoid showing red errors before the user has done anything.
