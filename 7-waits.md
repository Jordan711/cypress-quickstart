# Waits

In automated testing, it’s important to ensure elements are fully loaded before interacting with them.
Otherwise, your test might fail not because the element is missing, but because it wasn’t ready yet.

Cypress provides built-in wait mechanisms, including manual and smarter approaches.

### `cy.wait(milliseconds);`
- Pauses test execution for a specific number of milliseconds.
- Often used to give the page or specific actions time to complete.

Example:
```
cy.visit(url);

// Manually wait 5 seconds
cy.wait(5000);

// Then interact with the page
cy.get("button").click();
```

---

While `cy.wait()` can be useful in certain situations, relying on hardcoded delays is generally a bad practice.
- The app may take longer to load than expected, causing false test failures
- The app may load faster, causing unnecessary delay and slowing your test suite. As your test suite grows, these delays accumulate and increase total test time significantly.

## Intercepted Waits

Instead of waiting a fixed time, you can wait for a specific network request to complete using `cy.intercept()` and `cy.wait()` together.

This way, your test continues as soon as the actual data is ready — no guessing or hardcoding delays.

First, we'll need to intercept the specific request, and give it an alias
```
// Intercept the API call
cy.intercept("GET", "https://example.com/api/user").as("getUser");
```

Then pass the alias to cy.wait(), which tells Cypress to wait for that request to complete before continuing.
```
// Visit the page that makes the request
cy.visit("/dashboard");

// Wait for that request to finish
cy.wait("@getUser");

// Now safely interact with UI that depends on the data
cy.get(".user-info").should("contain", "Welcome");
```