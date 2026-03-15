```html
<!-- Text inputs -->
<input type="text"     name="username"  placeholder="johndoe" />
<input type="email"    name="email"     placeholder="you@example.com" />
<input type="password" name="password"  />
<input type="search"   name="q"         placeholder="Search..." />
<input type="url"      name="website"   placeholder="https://example.com" />
<input type="tel"      name="phone"     placeholder="+92 300 1234567" />

<!-- Numeric inputs -->
<input type="number" name="age"   min="1"   max="120" step="1" />
<input type="range"  name="vol"   min="0"   max="100" step="5" value="50" />

<!-- Date and time inputs -->
<input type="date"           name="birthday" />
<input type="time"           name="meeting"  />
<input type="datetime-local" name="event"    />
<input type="month"          name="expiry"   />
<input type="week"           name="week"     />

<!-- Selection inputs -->
<input type="checkbox" name="agree"  value="yes"   id="agree" />
<input type="radio"    name="theme"  value="light"  id="light" />
<input type="radio"    name="theme"  value="dark"   id="dark" checked />

<!-- File and color -->
<input type="file"  name="avatar"  accept="image/*" multiple />
<input type="color" name="accent"  value="#00add8" />

<!-- Hidden — submitted but not shown -->
<input type="hidden" name="csrf_token" value="abc123xyz" />

<!-- Buttons -->
<input type="submit" value="Submit Form" />
<input type="reset"  value="Clear Form" />
<input type="button" value="Click Me" onclick="doAction()" />
```

# Explanation

The `type` attribute on `<input>` is what determines the control's entire behaviour — appearance, keyboard, validation, and accepted values. HTML5 added many new types beyond the classic `text`, `checkbox`, and `radio`.

## Breakdown

- **`type="text"`**  
  Single-line plain text. The default type if `type` is omitted. No validation.

- **`type="email"`**  
  Validates email format (`user@domain.tld`). On mobile, shows an email-optimised keyboard with `@` and `.` keys prominent.

- **`type="password"`**  
  Masks characters as they are typed. Browsers offer to save passwords for this type.

- **`type="search"`**  
  Visually similar to `text` but semantically a search field. Some browsers add a clear (×) button. Pairs with `role="search"` on the parent form.

- **`type="url"`**  
  Validates URL format. Mobile shows a keyboard with `/` and `.com` shortcuts.

- **`type="tel"`**  
  No format validation (phone formats vary globally), but shows the numeric/phone keyboard on mobile.

- **`type="number"`**  
  Only accepts numeric input. `min`, `max`, and `step` constrain the value. Shows a numeric keypad on mobile.

- **`type="range"`**  
  A slider control between `min` and `max`. The `value` sets the default position. Submit value is the number.

- **`type="date"` / `type="time"` / `type="datetime-local"`**  
  Native date/time pickers. `date` submits ISO format (`2025-03-15`). `time` submits `HH:MM`. Browser support and styling vary significantly.

- **`type="checkbox"`**  
  A toggle. Multiple checkboxes with the same `name` allow multi-select. Only checked boxes are included in submitted data.

- **`type="radio"`**  
  Mutually exclusive selection within a group sharing the same `name`. Only the selected radio's `value` is submitted.

- **`type="file"`**  
  File upload control. `accept` filters shown file types (e.g., `image/*`, `.pdf,.doc`). `multiple` allows selecting more than one file.

- **`type="color"`**  
  A color picker. Value is a hex color string (`#rrggbb`). Default is `#000000`.

- **`type="hidden"`**  
  Invisible to the user but included in form submission. Used for CSRF tokens, session IDs, and pre-set values the user shouldn't modify.

## Key Points / Notes

- Always use the most specific `type` — it gives free validation, better mobile keyboards, and accessible semantics with zero extra code.
- `type="number"` still submits as a string — always parse it server-side.
- `type="date"` appearance cannot be easily styled cross-browser. Many production apps use a JavaScript date picker library for consistency.
- Multiple checkboxes with the same `name` — the server receives an array of the checked values.
- `type="radio"` groups are defined by sharing the same `name` — changing it creates a separate group.
