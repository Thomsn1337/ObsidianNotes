# Basic form validation

Form validation allows to set up constraints or rules that determine what data can be entered into an input. If such a rule is broken, a message will appear, providing feedback on the issues of the entered data and how to fix them.

Form validations are a vital part of forms. They allow to provide an easy user experience and to protect backend systems from receiving incorrect data.

## Required fields

Often times it is necessary to ensure that specific fields have been filled out before being able to submit the form. This can be achieved by adding the `required` attribute to any `input` element.

```html
<form>
	<label for="username">Username*</label>
	<input type="text" id="username" name="username" required>
</form>
```

To provide good user experience and to **meet accessibility guidelines**, there should always be some sort of indication that a field is required. This is commonly done by adding an asterisk `*` to the required field label.

## Text length

Sometimes it can be useful to define both a minimum and maximum amount of text that can be entered into a field. This can be achieved using the `minlength` and `maxlength` attributes respectively.

```html
<form>
	<textarea placeholder="What's happening?" minlength="5" maxlength="25">
	</textarea>
</form>
```

## Number range

Similar to text length validation, it is possible to limit the range of numbers that can be entered in a field. This can be achieved using the `min` and `max` attributes, which are also used to define the range of a `<input type="range">` field.

```html
<form>
	<input type="number" min="2" max="10" value="2">
</form>
```

## Pattern validation

To ensure that certain data like zip codes or credit card numbers are entered in the correct format, it is possible to define a pattern that the entered data has to match. This can be done using the `pattern` attribute with a **regular expression** as its value.

```html
<form>
	<label for="zip">Zip code</label>
	<input type="text" name="zip" id="zip" pattern="(\d{5}([\-]\d{4})?)" title="Please enter a valid zip code. Example: 65251">
</form>
```

The additional `title` attribute is used to provide a message when hovering over the input field. This message will also be displayed when a user tries to submit the form with invalid data entered.

When specifying a pattern for an input, it is common practice to provide a hint on what the data has to look like. This can be done using the above described `title` attribute. Another method can be using `placeholder`.

## Styling validations

To give better visual feedback if an input field has passed or failed a validation, it is possible to target them using the `:valid` and `:invalid` [CSS pseudo-classes](../../css/css_advanced_selectors.md).

This allows for more complex CSS operations. For example, it is possible to display an error message on the page if a validation fails.

```html
<form>
	<div class="input-field">
		<label for="password">Password</label>
		<input type="password" name="password" id="password" minlength="8">
		<span class="error">Pasword too short. Minimum 8 characters required.</span>
	</div>
</form>
```

```css
.input-field .error {
	display: none;
	color: red;
}

.input-field input:invalid ~ .error {
	display: block;
}
```

In this above example, the error message will only be displayed as long as the entered value of the password field is shorter than 8 characters.

The downside of this method is that the `:invalid` pseudo-class triggers on any failed validation, so if there are multiple validations on an input field, it doesn't allow for a simple way to display different messages depending on which validation failed. This would most likely require to use [JavaScript](../../javascript/basics/javascript.md) to create advanced validations.