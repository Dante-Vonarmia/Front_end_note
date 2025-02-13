# HTML Forms

## What are the new FORM elements which are available in HTML5?

### **The `progress` and `meter` Elements**

#### `meter`

The `meter` element provides for a gauge, displaying a general value within a range. \
It provide minimum (`min`) and maximum (`max`) values, and the required `value` that falls between those minimum and maximum values. \
While many think it’s a form control with attributes similar to some numeric input types, it has no `name` attribute and won’t be submitted on form submission.

#### `Progress`

The `meter` element should not be used to indicate progress; instead, use a `progress` bar to indicate the percentage of how complete a task is.\
Unlike `meter`, `progress` heads only in the direction of 100% of the `max` value. The presentation defaults to inline-block so you can set `width` and `height` on `progress` elements. Height will not change the actual height of the stylized bar (unlike `meter`) but will add space below it.

{% hint style="info" %}
If no `value` is included, the progress bar is indeterminate. Chrome, Opera, Safari, and Firefox display indeterminate progress as animated bars, with IE styling it as animated dots.
{% endhint %}

### **The `output` Element**

The purpose of the `output` element is to accept and display the result of a calculation. The `output` element should be used when the user can see the value, but not directly manipulate it, and when the value can be derived from other values entered in the form.&#x20;

An example use might be the total cost calculated after shipping and taxes in a shopping cart.\


### **The "`contenteditable`" Attribute**

While it is always best to use the most appropriate form element for its intended purpose, sometimes the existing form elements fall short of our needs.

For example, no form control makes for a good inline WYSIWYG text editor.

{% hint style="info" %}
Any element in an HTML5 document can be made editable with the `contenteditable` attribute. The `contenteditable` attribute, written simply as `contenteditable` or `contenteditable="true"`, makes the element on which it is included editable. You will usually find this attribute on divs, but you can even make a `style` element that’s set to `"display:block"` editable, and change CSS on the fly.
{% endhint %}

## **What** changes to Existing Form Controls?

### **The `form` Element**

#### **Variety types**

First, as we’ve seen, HTML5 provides a number of ways to natively validate form fields; certain input types such as `email` and `url`, for example, as well as the `required` and `pattern` attributes. You may, however, want to use these input types and attributes for styling or semantic reasons without preventing the form being submitted. The new Boolean `novalidate` attribute allows a form to be submitted without native validation of its fields.

#### No more Action

Next, forms no longer need to have the `action` attribute defined. You no longer need to explicitly state the URL to use it for form submission. If omitted, the form will behave as though the `action` were set to the current page. You can write or override the URL defined in the form’s `action` attribute with the `formaction` attribute of the button input types that activate form submission.

#### Autocomplete

Lastly, the `autocomplete` attribute we introduced earlier can also be added directly to the `form` element; in this case, it will apply to all fields in that form unless those fields override it with their own `autocomplete` attribute.

### **The `optgroup` Element**

In HTML5, you can have an `optgroup` as a child of another `optgroup`, which is useful for multilevel `select` menus.

### **The `textarea` Element**

In HTML 4, we were required to specify a `textarea` element’s size by specifying values for the `rows` and `cols` attributes. In HTML5, these attributes are no longer required; you should use CSS to define a `textarea`’s width and height

## **The miserable of submit and alter the value of a Radio Box and a Check box.**

> This problem could be the top 3 confusing problem happens to any beginner.\
> Anyway, my experience to you is simple.

Whenever **submitting** a checkbox or radio box. There are two part  need to be done if you wish to successful alter the **REAL** value of your input.

First, while we trigger the input, make sure you change the attribute: `value`.

Second, make sure you do alter the attribute `checked` in either this way:

```markup
<input type="radio" name="test-name2" checked>
```

&#x20;, or this way:

```markup
<input type="checkbox" name="test-name2" checked="checked">
```

by using JavaScript.

[A not quite easy sample here to follow.](https://www.dyn-web.com/tutorials/forms/examples/pizza.php)

## How use the value attribute with Radio Buttons and Checkboxes

Add the `value` attribute to the `input` elements of type `checkbox` and `radio`. Use the `input` label text, in lowercase, as the value for the attribute. The `value` attribute will make sure the choices are identifiable when the form is submitted.

Example form with value attributes:

```markup
<form>
  <label>
    <input id="indoor" value="indoor" type="radio" name="indoor-outdoor"> Indoor
  </label>
  <label>
    <input id="outdoor" value="outdoor" type="radio" name="indoor-outdoor"> Outdoor
  </label>
  <label>
    <input type="checkbox" name="personality" value="loving"> Loving
  </label>
  <label>
    <input type="checkbox" name="personality" value="lazy"> Lazy
  </label>
  <label>
    <input type="checkbox" value="energetic" name="personality" > Energetic 
  </label>
</form>
```

## How to check Radio Buttons and Checkboxes by Default

You can set a checkbox or radio button to be checked by default using the checked attribute. To do this, just add the word “checked” to the inside of an input element. For example,

```markup
<input type="radio" name="test-name" checked>
<input type="checkbox" name="test-name2" checked>
```

## What is a Boolean attribution of an `<input>` tag?

Some content attributes (e.g. `required`, `readonly`, `disabled`) are called [boolean attributes](https://www.w3.org/TR/html52/infrastructure.html#sec-boolean-attributes). If a boolean attribute is present, its value is **true**, and if it’s absent, its value is **false**.

HTML5 defines restrictions on the allowed values of boolean attributes: If the attribute is present, its value must either be the empty string (equivalently, the attribute may have an unassigned value), or a value that is an ASCII case-insensitive match for the attribute’s canonical name, with no leading or trailing whitespace. The following examples are valid ways to mark up a boolean attribute:

```markup
<div itemscope> This is valid HTML but invalid XML. </div>
<div itemscope=itemscope> This is also valid HTML but invalid XML. </div>
<div itemscope=""> This is valid HTML and also valid XML. </div>
<div itemscope="itemscope"> This is also valid HTML and XML, but perhaps a bit verbose. </div>
```

To be clear, the values "`true`" and "`false`" are not allowed on boolean attributes. To represent a false value, the attribute has to be omitted altogether. This restriction clears up some common misunderstandings: With `checked="false"` for example, the element’s `checked` attribute would be interpreted as **true** because the attribute is present.\
