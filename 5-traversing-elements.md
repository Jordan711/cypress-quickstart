# Traversing Elements

Cypress offers several powerful commands for navigating the DOM. Let's explore how to move through child and parent elements using some common traversal methods.

## Traversing Child Elements

Sometimes, elements on the page don't have a unique or easily identifiable selector — like an id or custom class.

For example:
```
<section>
    <button></button>
    <button></button>
    <form class="some-form">
        <button></button>
        <button></button>
        <button></button>
        <button></button>
    </form>
    <form class="two-form">
        <button></button>
        <button></button>
        <button></button>
        <button></button>
    </form>
</section>
```
Suppose we want to select the 3rd button inside `.two-form`, but none of the buttons have unique attributes.

**Strategy:**
We'll first select the parent `.two-form` and then grab the button from there using traversal methods.

---

Let's take a look at the following commands that may be useful in this case.

### `find(selector)`
- Searches all descendant elements of the current subject that match the provided selector
- Useful if the target element might be nested several levels deep.

### `children(selector)`
- Selects only direct children of the parent element.
- You can pass a selector to only return direct children of that type
- More precise and less likely to be affected by DOM changes.

### `eq(index)`
- Grabs an element at a specific zero-based index (first element is at index 0) from a list.

For example:
```
cy.get("button").eq(2);
```
This returns the 3rd button in the list.

Note: If the index is out of bounds (e.g., `.eq(5)` on a 3-item list), Cypress will throw an error.

---

So in this case, if we want to select the 3rd button of `two-form`, we can do something like

```
cy.get(".two-form").children("button").eq(2);
```

Why use `.children` instead of `.find`?

Using `.children("button")` ensures you're selecting only direct children. This makes your test more stable, especially if someone later adds nested elements like a `<div>` or wrapper inside `.two-form`.

---

## Traversing Parent Elements

Now, suppose you want to select the `<section>` that contains a specific button:
```
<section>
</section>
<section>
</section>
<section>
    <button class="super-button"></button>
</section>
<section>
</section>
<section>
</section>
```

### `parent()`
- Selects the direct parent of an element.
- Use it when you start from a known child and need to move upward in the DOM.


Using the `parent` method, we can get the correct `section` element by doing the following

```
cy.get(".super-button").parent();
```

This returns the `<section>` that directly contains the `.super-button`.