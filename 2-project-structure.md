# Cypress Project Structure

## Folder Structure
After generating the sample cypress project, let's look inside the `cypress` folder. Inside you would find 4 subfolders:
- downloads
    - This folder stores any files downloaded during your tests. For example, if your test clicks on a download link, the file will be saved here.
- e2e
    - This is where all your automated test scripts will live. These scripts contain the actual tests you want Cypress to run.
- fixtures
    - Fixtures contain static data that you can pass into your tests. For example, this can include mock data for different environments, users, or other test cases.
- support
    - The support folder contains helper files and functions to support your test scripts. This may include things like page objects, which encapsulate interactions with specific page elements, or custom commands that extend Cypress’s built-in functionality.

## Test Configuration

In addition, you might notice a new file called `cypress.config.js`
- This file holds global settings and environment variables for your tests

For example:
```
// cypress.config.js
module.exports = {
  e2e: {
    baseUrl: 'https://your-website.com',
    env: {
      username: 'testUser',
      password: process.env.CYPRESS_PASSWORD, // Password is fetched from an environment variable
    },
    viewportWidth: 1280,
    viewportHeight: 720,
  },
}
```

Side note: You may notice that the password field appears hidden or "funny" in the code. This is because passwords are considered sensitive information, and it's a best practice not to commit passwords in plaintext. Instead, we store them securely using environment variables to keep them out of version control and reduce the risk of exposing sensitive data.