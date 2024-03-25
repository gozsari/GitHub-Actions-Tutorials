Building on your introduction to GitHub Actions, the second lesson will focus on creating a **Continuous Integration (CI) Workflow**. Continuous Integration is a practice in software development where developers regularly merge their code changes into a central repository, after which automated builds and tests are run. GitHub Actions makes setting up CI workflows straightforward.

### Objective
Create a CI workflow that automatically builds and tests your code every time you push changes to the repository.

### Prerequisites
- Completion of the first lesson on GitHub Actions.
- A GitHub repository with a simple application that can be built and tested (e.g., a Node.js project, Python application, etc.).
- Basic understanding of your project's build and test commands.

### Lesson 2: Setting Up a Continuous Integration Workflow

**Step 1: Understanding CI Workflows**

- A CI workflow typically involves steps like setting up your project environment, installing dependencies, building your application, and running tests.
- The goal is to automate this process to ensure your codebase is consistently in a buildable and testable state.

**Step 2: Prepare Your Application**

- Ensure your application has a simple test setup. For instance, a Node.js project might have a few unit tests written with frameworks like Jest or Mocha.
- Verify that you can run these tests locally using a command (e.g., `npm test` for Node.js projects).

**Step 3: Create the CI Workflow File**

1. Inside the `.github/workflows` directory of your repository, create a new file named `ci-workflow.yml`.
2. Add the following content to your `ci-workflow.yml` file, adjusted to match your project's language and build/test commands:

```yaml
name: Continuous Integration Workflow

on: [push]

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2

    - name: Set up Node.js
      uses: actions/setup-node@v1
      with:
        node-version: '14'

    - name: Install dependencies
      run: npm install

    - name: Build
      run: npm run build # Replace this with your build command

    - name: Test
      run: npm test # Replace this with your test command
```

- Note: The above example is for a Node.js project. If your project uses a different stack, you'll need to adjust the setup steps and commands accordingly. For instance, Python projects might use `actions/setup-python` and run `pip install -r requirements.txt` to install dependencies.

**Step 4: Push Your Workflow**

- Commit the `ci-workflow.yml` file and push it to your GitHub repository:

```bash
git add .github/workflows/ci-workflow.yml
git commit -m "Add CI workflow"
git push origin main
```

**Step 5: Observe the CI Workflow in Action**

- After pushing your changes, go to the Actions tab of your GitHub repository. You should see the CI workflow running.
- Click on the workflow run to see detailed steps, including setup, build, and test commands.

### Conclusion

You've successfully created a CI workflow using GitHub Actions! This workflow automates the process of building and testing your code, providing immediate feedback on the integration status of your changes. As you develop more complex projects, consider enhancing your CI workflow with additional steps, such as code linting, security scans, or deploying to a staging environment.

In the next lesson, you might explore Continuous Deployment (CD) workflows to automate deploying your application to a production environment upon successful CI runs.