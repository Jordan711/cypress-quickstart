# Cypress Commands

## Basic Selectors
To interact with elements on a webpage, Cypress needs a way to locate them. This is where **selectors** come in.

Cypress uses commands like `.get()` and `.contains()` to select elements based on their CSS selectors or text content.

### `cy.get(selector)`

The `.get()` command selects one or more DOM elements using a **CSS selector**.

```
cy.get("[selector]");
```

To use this command, you'll need to pass in a CSS selector as an argument. Please refer to [this quick guide](https://www.w3schools.com/cssref/css_selectors.php) for a quick overview of how selectors work.

```
Common CSS Selectors:

div → selects all <div> elements.
#id → selects an element by its id.
.class → selects elements by class.
[attr=value] → selects elements by attribute.
```

Let's take [my website](https://jordanfeng.me/) for example:
If you want to select the "About Me" button by its ID:

```
cy.get("#about-toggle");
```
This targets the element with `id="about-toggle"`. Using IDs is ideal because they are typically unique for each element.

In contrast, something like:

```
cy.get("div");
```
would return all `<div>` elements, requiring additional filtering to find the right one.

---
### `cy.contains(text)`

The `.contains()` command selects elements based on their text content. It’s helpful when you want to interact with something you can visually identify by its label or text.

For example:
```
cy.contains("Work Experience");
```
This selects the first element on the page that contains the exact text "Work Experience" (case-sensitive).

Note: `.contains()` only returns the first match. Be careful if the text appears in multiple places.

```
// This could match any element with the word "the"
cy.contains("the"); 
```

### Combining `.contains()` with a Selector

To target a specific element type that contains specific text, you can combine both
```
cy.contains('button', 'Submit');
```
This selects the first `<button>` on the page that contains the text "Submit".

## Actions
After selecting the specific element we want, we can perform various actions on that element, including clicking, typing etc.

| Command | Description |
| --- | --- |
| `.click()` | Clicks the selected element |
| `.type()` | Types text into an input or textarea |
| `.clear()` | Clears the input field |
| `.dblclick()` | Double-clicks the selected element |

**Note:** Actions can only be used on **elements that support them**.

`.click()` should be used on clickable elements like `<button>`, `<a>`, `<label>`, etc

`.type()` and `.clear()` only work on inputs, textareas, or elements with editable content.

If you try to perform an action on an unsupported or invisible element, Cypress will throw an error.

#### Examples:

For example:
```
cy.get("#email").type("hello@example.com");
cy.get("button").click();
cy.get("input").clear();
cy.contains("Reset").dblclick();
```

## Assertions

Assertions verify that the application behaves as expected. In Cypress, you typically use `.should()` to make assertions about selected elements.

`.should()`

|Assertion|Meaning|
|---|---|
|`exist`|Element exists in the DOM|
|`be.visible`|Element is visible|
|`have.text`|Element has exact text content|
|`contain`|Element contains specific text|
|`have.value`|Input has a specific value|
|`have.attr`|Element has a given attribute and value|
|`have.class`|Element has a specific class|
|`be.enabled`|Element is enabled (not disabled)|
|`be.disabled`|Element is disabled|
|`be.checked`|Checkbox or radio button is checked|

So, to verify an input field has specific text:
```
cy.get("input").should("have.value", "hello@example.com");
```

And to verify that a button is visible and enabled:
```
cy.get("button").should("be.visible").and("be.enabled");
```