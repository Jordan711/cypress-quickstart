# Cypress Installation

## Prerequisites
Ensure that Node.js and npm (Node Package Manager) are installed on your system. npm comes bundled with Node.js, so installing Node.js will automatically install npm.
- Node.js
    - https://nodejs.org/en

After installing, you can verify that they are installed and functioning by opening command prompt and then running the following commands

```
node -v
npm -v
```

What this does is that it prints the current version of node, and npm. If it throws an error, that means something went wrong. Try reinstalling and running those commands again.

## Installing Cypress

1. Create a new folder where your Cypress project will reside. This could be anywhere on your machine.

2. Open your command prompt or terminal, and use the cd command to navigate to the folder you just created. 

```
cd <path to the folder>
```

3. Install Cypress using the following command
- This will install Cypress and add it to the devDependencies in your package.json
```
npm install --save-dev cypress
```

## Generating Example Tests
You may notice that after running the npm install command, the project folder only contains the following
- package.json
- node_modules
- package-lock.json

To avoid starting from scratch, you can generate example tests easily by following these steps:

First, run the following command, which opens the Cypress GUI
```
npx cypress open
```
This should open a Cypress window. 

1. In the window, click E2E Testing. 

2. It will automatically generate the configuration files. Click Continue.

3. Select any browser, and then click Start E2E Testing

4. When the browser opens, you'll have two options for generating example test files. Click Scaffold example specs to automatically generate a series of test files covering basic to advanced usage examples.

5. After that, click on any of the files to watch it run the test!

## Running Cypress
There are two ways to run Cypress

### Open the Cypress UI (Interactive Mode)

This is the method we used earlier to generate example tests. This command opens the Cypress Test Runner (UI), where you can select which tests to run and visually see the tests being executed in real-time. You also get useful debugging tools like screenshots, videos, and logs.
```
npx cypress open
```
### Run Cypress in Headless Mode (Command Line)

If you have existing tests, you can run them without seeing the UI. This will run the tests in headless mode, and the results will be printed in the command prompt (or terminal) after completion.

```
npm cypress run
```

## Customizing Cypress Runs with Flags

With the run command, since there's no UI that lets you control how tests are specifically run, you can also customize how the tests are run with different flags. Here are some commonly used ones

### Run Specific Tests with the --spec Flag
If you only want to run specific test(s), you can customize it with this flag
```
--spec <path to file or folder>
```

### Choose a Specific Browser with the --browser Flag
If you want to choose the browser, use this flag
```
--browser <browser>
```
To use those flags, you would just add them to the end of the command.

For example, if I only want to run test.cy.js, I would do something like

```
npx cypress run --spec cypress/e2e/test.cy.js --browser chrome
```