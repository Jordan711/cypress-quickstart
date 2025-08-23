# Cypress Test Structure

Let's go to `cypress/e2e/1-getting-started/todo.cy.js` and  open the `todo.cy.js` file in a code editor (Any is fine, but I recommend VS Code).

This file doesn't include any import statements by default because Cypress automatically provides global access to many commands. However, in a typical project, you might add your own imports (e.g., utility functions or fixtures) at the top.

Inside this file, you'll see several blocks of code, wrapped in curly brackets, to organize the test logic:
- `describe`
    - This block groups together related tests. Everything inside it describes the feature or functionality you are testing
- `beforeEach`
    - This block contains code that runs before each individual test in the file. It's useful for setting up any preconditions or shared setup steps for your tests
- `it`
    - This block represents an individual test case. It contains the logic for a specific behavior you are testing, like "should add an item to the to-do list."
- `context`
    - `context` is functionally identical to describe. It’s often used to make tests more readable when describing different conditions or scenarios (e.g., 'when the user is logged in').

## Additional Commonly Used Hooks
`beforeEach` runs before each individual test, but there are also additional hooks for controlling test flows
- `afterEach`
    - Runs after each test, this can be useful for clearing data or resetting the test environment before the next test
- `before`
    - This is a bit different from beforeEach.
    - `before` runs once before all tests in a describe or context block. It's useful for one-time setup tasks, like creating test data.
- `after`
    - Similar to `before` this only runs once, after all the tests have been run in a describe or context block.
    - For example, this can be useful for cleanup tasks that should only happen once after all tests have run, such as closing sessions, deleting test data, or performing analytics

## Controlling Test Runs
During test development, you may want to control which tests are skipped, or maybe only run certain test cases. 

- `only`
    - This keyword tells Cypress to run only the specific test or block it’s attached to, ignoring all other tests
    - To use this, add `.only` after the `it` or `describe` block
```
it.only('should add an item to the todo list', () => {
  cy.get('input').type('Buy Milk');
  cy.get('button').click();
  cy.get('ul').should('contain', 'Buy Milk');
});
```
- `skip`
    - This keyword tells Cypress to skip that test or block
    - To use this, add `.skip` after the `it` or `describe` block
```
it.skip('should not add an invalid item to the todo list', () => {
  cy.get('input').type('');
  cy.get('button').click();
  cy.get('ul').should('not.contain', '');
});
```