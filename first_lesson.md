
**Introduction to GitHub Actions and Setting Up Your First Workflow**.

### Objective
Understand the basics of GitHub Actions and create a simple workflow that executes when code is pushed to your repository.

### Prerequisites
- A GitHub account.
- Basic familiarity with Git and GitHub.
- A repository on GitHub you can use for testing (it can be empty or an existing project).

### Lesson 1: Creating Your First GitHub Action Workflow

**Step 1: Introduction to GitHub Actions**

- GitHub Actions helps automate tasks within your software development lifecycle. GitHub Actions are event-driven, meaning you can run a series of commands after a specified event has occurred, such as pushing code to a repository or creating a pull request.
- Workflows are defined in `.yml` or `.yaml` files within the `.github/workflows` directory of your repository.

**Step 2: Set Up Your Repository**

- If you don't already have a GitHub repository, create one by clicking the "New" button on the GitHub homepage after logging in.
- Clone the repository to your local machine using Git.

**Step 3: Create Your First Workflow**

1. In your repository, create a directory named `.github/workflows`. You can do this locally on your machine and then push the changes to GitHub.
2. Inside the `workflows` directory, create a new file named `hello-world.yml`.
3. Add the following content to your `hello-world.yml` file:

```yaml
name: Hello World Workflow

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Run a one-line script
      run: echo Hello, world!
    - name: Run a multi-line script
      run: |
        echo Add other commands you want to run here
        echo This is a multi-line script
```

4. Commit your changes and push them to GitHub:

```bash
git add .github/workflows/hello-world.yml
git commit -m "Add hello world workflow"
git push origin main
```

**Step 4: Trigger Your Workflow**

- Your workflow will trigger automatically upon pushing your changes to GitHub. In this case, it's set to run on every push event to any branch.
- To see your workflow in action, go to your GitHub repository > Actions tab. You should see the "Hello World Workflow" running or completed successfully.

**Step 5: Review Your Workflow's Results**

- Click on the workflow run to see more details. You can see each step executed, including the "Hello, world!" output from our script.

### Conclusion

Congratulations! You've just created and run your first GitHub Action workflow. This basic workflow introduces you to the concept of automating tasks using GitHub Actions. As you progress, you'll find that you can automate more complex workflows, including building, testing, and deploying your applications.

For your next lesson, consider diving into more complex workflows, such as setting up CI/CD pipelines for your application, running tests automatically, or deploying your code to a server.