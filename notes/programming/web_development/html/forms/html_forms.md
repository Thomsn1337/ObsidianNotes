# Forms

Forms are the user's gateway into the backend. They allow the user to enter some data that can be progressed and sent to the server. Forms consist of multiple different [HTML elements](html_elements_tags.md).

## The form element

The `<form>` element is a simple container element similar to the `<div>` element, but it has a mayor difference. It accepts two special [attributes](html_attributes.md) in addition to the normal ones, called `action` and `method`. 

The `action` attribute takes an URL as its value and tells the form where the entered data should be sent to so it can be processed.

The `method` attribute defines which type of [HTTP request](../../../software_design_and_principles/http_requests.md) should be performed.

Since the `<form>` element is only a container, it needs some additional elements that allow the user to interact and to enter data. Such elements can be text boxes, dropdowns, checkboxes or buttons.

## The input element

The `<input>` element is the most common and most versatile form control element. This element is a self-closing tag. It accepts a `type` attribute, which defines the type of data collected by the field. Some of the available input types are:

- `text`: a normal text field.
- `email`: specialized text input for email addresses. They require an `@` sign to be present in order to submit the form. Additionally they display a special keyboard on mobile devices which includes an `@` sign to make entering email addresses easier.
- `password`: specialized text input which masks the entered data with other characters, which is generally used for sensible information like passwords.
- `number`: only accepts numbers and ignores any other entered characters.
- `date`: renders a date picker calendar to allow the user to enter a date value.
- `radio`: used to make a selection from existing options. Displays a radio button per option, of which only one can be selected at the same time. They are commonly used when there are less than 5 possible selections.
- `checkbox`: similarly to radio buttons, they allow to select from multiple options. The difference is, that checkboxes allow for multiple selections at once.
- `range`: displays a slider to select a value between a defined minimum and maximum. The range can be defined using the `min` and the `max` attributes.

A list of some additional input types can be found [here](https://www.w3schools.com/html/html_form_input_types.asp).

```html
<form>
	<input type="text">
	<input type="password">
</form>
```

In addition to the `type` attribute, there has to be an `id` and a `name` attribute to an input field, or really any form control element. These two attributes are commonly set to the same value.

The `id` will be used to link a label to the input field.

The `name` serves as a reference to the form control when submitting it to the backend. It can be thought of as a variable name for the input. If there is no `name` attribute present, the value will be ignored when submitting the form.

```html
<form>
	<input type="text" name="username" id="username">
	<input type="password" name="password" id="password">
</form>
```

More optional attributes for `<input>` elements can be found [here](https://www.w3schools.com/html/html_form_attributes.asp).

## Text areas

The `<textarea>` element provides a input box similar to an `<input type="text">`, but it accepts text that spans over multiple lines. It also allows to be resized by dragging from the bottom right corner.

Unlike `<input>` elements, the `<textarea>` element has a closing tag, which allows to wrap some initial content to display other than just a placeholder.

```html
<form>
	<textarea rows="30" cols="40">Sample text</textarea>
</form>
```

The optional `rows` and `cols` attributes can be used to define the initial size of the text field.

## Selections

The `<select>` element allows to select a value from a predefined list. It renders a dropdown list with the predefined values.

The `<select>` element is only a wrapper, similar to an unordered or ordered list. For each selectable option, there has to be an `<option>` element inside of it.

```html
<select name="car">
	<option value="toyota">Toyota</option>
	<option value="mercedes">Mercedes</option>
	<option value="bmw">BMW</option>
	<option value="audi">Audi</option>
</select>
```

Just like the `<input>` element, the `<select>` element should have a `name` attribute.

The `<option>` element should have a `value` attribute. This attribute defines the value that will be passed when the form submits. The text inside the tags will be displayed in the dropdown. If the `value` attribute is missing, the text content inside the tags will be used.

The options inside the `<select>` element can be grouped together logically using the `<optgroup>` element. Using this, the options will be separated by labels.

```html
<select name="fashion">
	<optgroup label="Clothing">
	    <option value="t_shirt">T-Shirts</option>
	    <option value="sweater">Sweaters</option>
	    <option value="coats">Coats</option>
	</optgroup>
	<optgroup label="Foot Wear">
	    <option value="sneakers">Sneakers</option>
	    <option value="boots">Boots</option>
	    <option value="sandals">Sandals</option>
	</optgroup>
</select>
```

## Labels

The `<label>` element allows to give each input field a descriptive title, so the user knows what type of data he is expected to enter.

```html
<form>
	<label for="first-name">First name</label>
	<input type="text" name="first-name" id="first-name">
</form>
```

The label takes in a `for` attribute. It will associate with an input field which `id` value matches with the value of the `for` attribute. This allows to activate the corresponding input field when clicking on a label.

## Buttons

While also used for many other things, buttons are the main method to submit a form. They can be created using the `<button>` element. This element can take in a `type` attribute which defines the use case of the button.

A generic button with any use case can be created by setting `type="button"`. This is the default value.

```html
<button type="button">Click me</button>
```

A button for submitting a form can be created by setting `type="submit"`.

```html
<form>
	<label for="username">Username</label>
	<input type="text" name="username" id="username">

	<label for="password">Password</label>
	<input type="password" name="password" id="password">

	<button type="submit">Submit</button>
</form>
```

It is also possible to create a *reset* button by setting `type="reset"`. Clicking this will clear all the entered data and reset all the input fields to their initial values.

```html
<form>
	<label for="username">Username</label>
	<input type="text" name="username" id="username">

	<label for="password">Password</label>
	<input type="password" name="password" id="password">

	<button type="reset">Reset</button>
	<button type="submit">Submit</button>
</form>
```