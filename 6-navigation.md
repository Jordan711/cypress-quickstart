# Navigation

Cypress allows us to navigate different pages with the following methods

`cy.visit(url)`
- Navigates to the specified URL
- This is typically the first command in most tests, and is used to load the page you want to test.
```
cy.visit("https://jordanfeng.me");
```

`cy.reload()`
- Reloads the current page
```
cy.reload();
```
- Passing `force: true` performs a hard reload (ignoring browser cache)
```
cy.reload({ force: true });
```

`cy.go(number)`
- Navigates through the browser's history stack
    - Use negative numbers to go back
    - Use positive numbers to go forward
```
// Go back once
cy.go(-1);

// Go back 3 times
cy.go(-3);

// Go forward once
cy.go(1);
```

---

## Verifying URL

After navigating, you can use the `cy.url()` command to verify the current page.

`cy.url()`
- Returns the full current URL as a string

So you can do something like this to check the url:
```
// Check for exact match
cy.url().should("eq", "https://jordanfeng.me/");

// Check that URL includes a specific path
cy.url().should("include", "/dashboard");
```

---

Alternatively, `cy.location()` allows you to verify specific parts of the url.
- `href`
- `pathname`
- `host`
- `hostname`
- `protocol`
- `port`

### Examples
```
// Verify full url (same as cy.url())
cy.location('href').should('eq', 'https://example.com/dashboard');

// Verify pathname
cy.location('pathname').should('eq', '/dashboard');

// Verify protocol
cy.location('protocol').should('eq', 'https:');

// Verify hostname
cy.location('hostname').should('eq', 'example.com');
```