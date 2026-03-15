```html
<!-- Basic dropdown -->
<label for="country">Country</label>
<select id="country" name="country">
  <option value="">-- Choose a country --</option>
  <option value="pk">Pakistan</option>
  <option value="us">United States</option>
  <option value="gb">United Kingdom</option>
</select>

<!-- Grouped options -->
<select name="city">
  <optgroup label="Asia">
    <option value="khi">Karachi</option>
    <option value="lhr">Lahore</option>
  </optgroup>
  <optgroup label="Europe">
    <option value="ldn">London</option>
    <option value="par">Paris</option>
  </optgroup>
</select>

<!-- Multi-select (hold Ctrl/Cmd to select multiple) -->
<select name="skills" multiple size="4">
  <option value="html">HTML</option>
  <option value="css" selected>CSS</option>
  <option value="js" selected>JavaScript</option>
  <option value="go">Go</option>
</select>

<!-- Textarea — multi-line text -->
<label for="bio">Bio</label>
<textarea
  id="bio"
  name="bio"
  rows="6"
  cols="50"
  maxlength="500"
  placeholder="Tell us about yourself..."
></textarea>

<!-- Button types -->
<button type="submit">Submit the Form</button>
<button type="reset">Clear All Fields</button>
<button type="button" onclick="openModal()">Open Modal</button>

<!-- Button with icon -->
<button type="submit">
  <img src="send-icon.svg" alt="" />
  Send Message
</button>

<!-- Disabled button -->
<button type="submit" disabled>Processing...</button>
```

# Explanation

`<select>`, `<textarea>`, and `<button>` are the three remaining core form controls. Together with `<input>`, they cover every kind of user input — from dropdowns to free text to form submission.

## Breakdown

- **`<select>`**  
  A dropdown menu. The `name` attribute is the key submitted. Each `<option>` has a `value` (what is submitted) and display text (what the user sees). Without a `value`, the display text is submitted.

- **`<option value="">`** (blank first option)  
  A placeholder prompt like "-- Choose --". Setting `value=""` means the field is empty when this is selected — pairs with `required` to force a real selection.

- **`selected` attribute on `<option>`**  
  Sets the pre-selected option. If omitted, the first option is selected by default.

- **`<optgroup label="...">`**  
  Groups related options under a non-selectable heading. Greatly improves readability for long dropdowns.

- **`multiple` on `<select>`**  
  Allows selecting more than one option (Ctrl/Cmd+click). The server receives multiple values for the same key. `size` sets how many options are visible without scrolling.

- **`<textarea>`**  
  A free-form multi-line text input. `rows` and `cols` set the initial size (override with CSS). `maxlength` caps the character count. Leave no whitespace between the opening and closing tags — any whitespace becomes part of the value.

- **`<button type="submit">`**  
  Submits the parent form. This is the default type — a `<button>` with no `type` attribute behaves as `submit`, which causes surprising bugs when used inside forms for non-submit purposes.

- **`<button type="reset">`**  
  Resets all form controls to their default values. Use sparingly — accidentally clicking reset after filling a long form is frustrating UX.

- **`<button type="button">`**  
  Does nothing by default. Used with JavaScript (`onclick`, event listeners) for actions that should not submit or reset the form.

- **`disabled` attribute**  
  Prevents interaction and excludes the control from form submission. Style with CSS to indicate the disabled state visually.

## Key Points / Notes

- `<button>` is richer than `<input type="submit">` — it can contain HTML (icons, images, formatted text), not just a plain text label.
- Always set `type="button"` on any `<button>` inside a form that isn't meant to submit it — the default `submit` type causes unintended form submissions.
- For `<textarea>`, `rows` and `cols` are just the initial size. Always set `resize: vertical` or `resize: none` in CSS to control whether users can resize it.
- `<textarea>` has no `value` attribute — its initial content goes between the opening and closing tags.
- Multi-select `<select>` has notoriously poor UX on mobile. Consider checkboxes as an accessible alternative for small option sets.
