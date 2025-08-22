# Cypress Commands

## Basic Selectors
In order to interact with the elements on the webpage, we first need to grab the element. How do we tell Cypress how to locate and interact with a specific element? 

In Cypress, one of those selectors is `.get()`.
To use this command, you'll need to pass in a CSS selector as an argument. Please refer to [this quick guide](https://www.w3schools.com/cssref/css_selectors.php) for a brief summary on how to select elements eithin a page.

In summary,

```
 --> element
# --> id
. --> class
[] --> attribute
```

Let's take [my website](https://jordanfeng.me/) for example:
If I wanted Cypress to select the first button (About Me), then I would do something like this

```
cy.get("#about-toggle");
```
In the example above, I decided to grab the button using its id, because ids should be unique to each specific element. If I did something like

```
cy.get("div");
```
That would just return a list of all the `div` elements, which would require additional effort to sort through in order to find the exact element I want.

---

In addition to `.get`, we also have the `.contains` command, which grabs the element based on their text content. 

For example:
```
cy.contains("Work Experience");
```
This would grab the first element on the page that has the exact words and capitalization, "Work Experience".

Note: `contains` only returns the first DOM element that contains the specified text. So you need to make sure that the text you want to search, only appears for the element you want.

E.g. This would select the element with the first occurence of 'the', which can be any element
```
cy.contains("the");
```

Now there can be occurrences where multiple elements on the page have the same text, but you still want to grab a specific element. Fortunately, with `contains`, you can combine both a selector and the text you want to look for.
```
cy.contains('button', 'Submit');
```
This grabs the first occurence of a button element, that also has the text "Submit".

## Actions
After selecting the specific element we want, we can perform various actions on that element, including clicking, typing etc.

`.click()`

`.type()`

`.clear()`

`.dblclick()`

## Assertions

In addition to actions, we can also verify information in the selected elements. For this, we use assertions

`.should()`

exist, be.visible, have.text, contain, have.value, have.attr, have.class, be.enabled, be.disabled, be.checked