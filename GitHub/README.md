# GitHub

**What is GitHub Actions?**

GitHub Actions is a CI/CD service provided by GitHub that allows you to automate workflows directly within your GitHub repositories.

**Workflows** 
You define workflows in YAML files stored in the .github/workflows directory of your repository. Each workflow can consist of multiple jobs that can run sequentially or in parallel.

**Triggers**
Workflows can be triggered by various GitHub events, such as code pushes, pull requests, issues, releases, and more. You can also schedule workflows or trigger them via API calls.

**Jobs and Steps**
Each workflow is composed of jobs, which run on specified virtual environments (like Ubuntu, Windows, or macOS). Jobs contain steps, which can include shell commands, actions, or scripts.

**Example Use Cases:**
- Continuous Integration: Automatically run tests and build your application whenever code is pushed to the repository.
- Continuous Deployment: Deploy code to production or staging environments after successful tests.
- Automated Code Quality Checks: Lint code or run static analysis on pull requests.
- Notifications: Send alerts or updates to team members based on repository events.

**Actions** are reusable pieces of code that automate specific tasks within your workflows.

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run Tests
        uses: my-org/run-tests@v1  # This is your reusable action
```

**Marketplace:** GitHub provides a marketplace where developers share their actions. You can find actions for common tasks, like deploying to cloud providers, sending notifications, or managing dependencies, and easily incorporate them into your workflows.

Secrets Management: You can store sensitive information, like API keys and tokens, securely in GitHub Secrets and reference them in your workflows.

```yaml

password: ${{ secrets.secret_name }}

```

**Caching Techniques**

Caching in GitHub Actions is a technique used to store and reuse files or dependencies between workflow runs to speed up subsequent builds. By caching certain files, you can avoid downloading or generating them each time a workflow runs, which can significantly reduce execution time and improve efficiency.

- Caching Step: The actions/cache action is used to cache the node_modules directory. The cache key is based on the operating system and a hash of the package-lock.json file, which means the cache will be updated if dependencies change.

```yaml
name: CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Cache Node.js modules
        uses: actions/cache@v2
        with:
          path: node_modules  # Path to cache
          key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}  # Cache key

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

**Matrix Build**

Allows you to run multiple versions of your job in parallel like in different OS

```yaml
name: Node.js CI

on: [push, pull_request]

jobs:
  build:
    runs-on: ${{ matrix.os }}  # Use the operating system from the matrix

    strategy:
      matrix:
        os: [ubuntu-latest, windows-latest]  # Define the OS matrix
        node-version: [12, 14, 16]           # Define the Node.js version matrix

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v2
        with:
          node-version: ${{ matrix.node-version }}  # Use the Node.js version from the matrix

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

**Run multiple commands in a single Step**

```yaml
steps:
  - name: Run multiple commands
    run: |
      echo "Step 1: Install dependencies"
      npm install
      echo "Step 2: Run tests"
      npm test
```

**Workflow that builds a Docker image and pushes it to a Docker registry**

```yaml
name: Build and Push Docker Image

on:
  push:
    branches:
      - main  # Trigger on pushes to the main branch
  pull_request:
    branches:
      - main  # Trigger on pull requests to the main branch

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Docker Buildx
        uses: docker/setup-buildx-action@v1

      - name: Log in to Docker Hub
        uses: docker/login-action@v1
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build Docker image
        run: |
          docker build -t myusername/myimage:latest .

      - name: Push Docker image
        run: |
          docker push myusername/myimage:latest

```
