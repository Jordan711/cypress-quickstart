# Good Selector Practices

In automated testing, selectors should be written in a way that keeps tests stable — even when the application’s layout or styling changes.

The goal is to ensure that tests only fail when there’s a real functional problem, not due to unrelated visual or structural updates.
- Tests that rely on brittle selectors (like class names or DOM structure) can easily break when the UI changes
- A test should fail only when the functionality breaks, not because of unrelated layout or styling changes

## Best Practices for Writing Selectors

### Using `data-*` Attributes
If available, it is recommended to use `data-*` attributes. 

`data-cy` is the most commonly used one but others like `data-test`, `data-testid` and more could also be used.

These attributes are meant for testing and don’t get affected by CSS or layout changes.

For example, with the following element
```
<button data-cy="submit-button">Submit</button>
```

You would select it by doing the following
```
cy.get('[data-cy=submit-button]').click();
```

If your app doesn’t already include these attributes, consider adding them specifically for testing purposes. 

---

### Avoid Relying on CSS Classes
Styling changes frequently during application development, so relying on CSS classes often leads to brittle selectors, since these are likely to change whenever styles are updated.

AVOID:
```
cy.get('.btn.btn-primary').click();
```

If class names are your only option (e.g., no IDs or `data-*` attributes), use stable, meaningful class names:
```
<button class="submit-button">Submit</button>
```
In this case, the class name is meaningful and unlikely to change — making it a safer choice.

---

### Avoid Exact Nested Selectors
Selectors that rely on exact parent-child relationships are fragile, since even minor layout changes can break them.

AVOID:
```
cy.get('form > div:nth-child(2) > input').type('value');
```

Try this instead:
```
cy.get('form#login-form').find('input[name="email"]').type('test@example.com');
```

By using additional identifiers like a form `id` and an input `name`, you make your selectors more specific and resilient — especially when there are multiple similar forms or fields on the page.

---

### Additional Tips
If `data-*` attributes or stable class names aren't available, consider using accessible attributes like `name`, `placeholder`, or associated text.

For example:
```
cy.get('input[placeholder="Email"]')...
cy.contains('button', 'Submit')...
```

Try to avoid using `.eq()`, because that relies on exact positioning (index) of an element. Positional selectors are fragile and often break when new elements are added or the layout changes.

---

## General Selector Preference Ranking
1. `data-*cy*` Attributes
2. ID Attributes
3. Meaningful Class Names
4. `name`, `placeholder`, `aria-label`
5. Text content `.contains()`
    -  Is vulnerable to text changes
6. Element selectors `button`, `input`
    - Generic and prone to selecting multiple elements unintentionally