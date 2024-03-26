Building on the foundation of understanding GitHub Actions and automating tests, the third practical lesson focuses on **Deploying Your Application with GitHub Actions**. This lesson will guide you through creating a workflow to deploy your application to a server after a successful build and test process.

### Objective
Learn how to automate the deployment of your application using GitHub Actions, ensuring that only successfully tested builds are deployed.

### Prerequisites
- Completion of the previous lessons on GitHub Actions.
- A GitHub repository with an application that includes a working GitHub Action for CI tests.
- Access to a deployment target (e.g., a virtual server, cloud provider like AWS, Azure, Heroku, or a service like Netlify or Vercel).

### Lesson 3: Automating Deployment

For the purpose of this lesson, we will assume a simple web application that we'll deploy to a cloud service (Heroku as an example). The principles applied here can be adapted to other environments or providers.

**Step 1: Prepare Your Deployment Target**

- Ensure you have an account on Heroku and have created an application there. Note the application name, as it will be used in the deployment process.
- Install the Heroku CLI locally and authenticate it with your Heroku account.

**Step 2: Store Deployment Credentials Securely**

- In your GitHub repository, go to Settings > Secrets, and add your deployment credentials as secrets. For Heroku, you will need `HEROKU_API_KEY` and `HEROKU_APP_NAME`.

**Step 3: Create a Deployment Workflow**

1. In your repository’s `.github/workflows` directory, create a new file named `deploy.yml`.
2. Add the following content to `deploy.yml`, adjusting the deployment steps based on your specific deployment target and requirements:

```yaml
name: Build, Test, and Deploy

on:
  push:
    branches:
      - main  # Adjust this to match your default branch if it's not 'main'

jobs:
  build-and-test:
    runs-on: ubuntu-latest

    steps:
    - uses: actions/checkout@v2
    - name: Set up Node.js
      uses: actions/setup-node@v2
      with:
        node-version: '14'  # Adjust this as per your project's requirements

    - name: Install Dependencies
      run: npm install

    - name: Run Tests
      run: npm test

  deploy:
    needs: build-and-test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main' && success()  # Ensures deployment runs only if build and test are successful and on the main branch
    steps:
    - uses: actions/checkout@v2

    - name: Heroku Deploy
      uses: akhileshns/heroku-deploy@v3.12.12  # This is a community action for Heroku deployment
      with:
        heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
        heroku_app_name: ${{ secrets.HEROKU_APP_NAME }}
        heroku_email: your-email@example.com  # Replace with your Heroku account email
```

**Step 4: Commit and Push Your Workflow**

- Commit your changes and push the `deploy.yml` file to your repository:

```bash
git add .github/workflows/deploy.yml
git commit -m "Add deployment workflow"
git push origin main
```

**Step 5: Verify Your Workflow**

- Upon pushing your changes, the GitHub Actions workflow will trigger, running through the build, test, and deployment phases.
- You can monitor the progress and outcome in the Actions tab of your GitHub repository.

### Conclusion

You've now automated the entire process from code push, through building and testing, to deploying your application using GitHub Actions. This CI/CD pipeline ensures that every change is automatically tested and deployed, streamlining your development workflow and reducing the potential for human error.

For further exploration, consider adapting the workflow to different deployment environments, implementing rollback strategies, or incorporating more complex deployment conditions. Each improvement will further solidify your understanding of DevOps practices and GitHub Actions.