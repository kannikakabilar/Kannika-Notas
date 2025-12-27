<h1 style="color:#ff4b19">GitHub</h1>

Note: Need to learn about inputs and outputs in GitHub Actions

<h3 style="color:#ff4b19">What is GitHub Actions?</h3>

GitHub Actions is a CI/CD service provided by GitHub that allows you to automate workflows directly within your GitHub repositories.

<h3 style="color:#ff4b19">Workflows</h3>
You define workflows in YAML files stored in the .github/workflows directory of your repository. Each workflow can consist of multiple jobs that can run sequentially or in parallel.

<h3 style="color:#ff4b19">Triggers</h3>
Workflows can be triggered by various GitHub events, such as code pushes, pull requests, issues, releases, and more. You can also schedule workflows or trigger them via API calls.

```yaml
name: "(Single-card) Demo tests"  # Quotes are needed when using special characters like: () []  {} : , & * # ' " leading or trailing spaces

on:  # Under this 'on' section, you can define various event triggers

  workflow_dispatch:  # allows you to manually trigger the workflow

  schedule:  # gets triggered on a set schedule
    - cron: '*/10 * * * *'  # runs every 10 minutes
  
  push:  # This workflow will get triggered when a commit is pushed to main or the dev branches
    # Block style
    branches: [main, dev]  # mention the branch names here
    paths:  # optional/use-as-needed the option triggers the workflow if there's a push to main AND changes include files inside mentioned path
      - '.github/workflows/**'
    # Flow style
    branches:  # both styles function the same
      - main
      - dev

  pull_request:  # By default, having this will trigger this workflow if a PR is created (Draft or Open), when a new commit is pushed to the PR branch, when a closed PR is reopened
    branches: [main]  # When a PR is created to be merged to main
    # You can customize the types filter
    types:
      - opened
      - synchronize  # when a new commit is pushed to the PR branch
      - reopened
      - ready_for_review  # Draft converted to ready
      - closed # PR closed (merged or not)
      - assigned # (or unassigned) assignee changes
      - labeled  # (or unlabeled) assignee changes
      - edited

  # Note: pull_request is different from pull_request_target in the following ways
  # Repo checkout:
  #  pull_request checks out PR branch code
  #  pull_request_targe checks out base branch code (the branch you are merging to) by default unless you explicitly mention it
  # Secrets Access:
  #  pull_request cannot access secrets when triggered from a fork
  #  pull_request_target full access to secrets even when triggered from a fork
  # Permission:
  #  pull_request read-only from forks
  #  pull_request_target write access to repos
  # Overall use pull_request_target when running safe trusted workflows or for bot automation that needs repo write access

  workflow_call:  # Makes the workflow reusable (can be called by other workflows)
    inputs:
      nameOfInput1:
        description: "Please enter input1 value"
        required: true
        default: 1
        type: number
  workflow_run:  # Triggers when another workflow runs
    workflows:
      - "Package and release"
      - "(Single-card) Frequent model and ttnn tests"

  repository_dispatch:  # is a webhook-based trigger that allows you to remotely trigger a workflow via a GitHub API
    types: [trigger-llk-update]
    # And this is how you can trigger the workflow - You send a POST request to GitHub's API with a custom event type 
    # which has to be trigger-llk-update and any other event type trigger won't work
    # curl -X POST \
    #   -H "Accept: application/vnd.github+json" \
    #   -H "Authorization: Bearer YOUR_TOKEN" \
    #   https://api.github.com/repos/OWNER/REPO/dispatches \
    #   -d '{"event_type":"trigger-llk-update","client_payload":{"key":"value"}}'

  merge_group:  # Runs on merge queue events
    types:
      - checks_requested  # When PR enters or moves in the merge queue (The workflow runs tests on tmp commit with the merged code PR+main+any_PRs_queued_above)
      - destroyed  # When the PR leaves the merge queue

  # Other event triggers
  issues, issue_comment:  # issue activity
    types: [created]
  release, published, created:  # Release-related events
  pull_request_review, pull_request_review_comment:  # PR review events
    types: [created, submitted]
  create, delete:  # Branch/tag creation/deletion
  fork:  # Repo fork events
  watch:  # Repo starred events
  deployment, deployment_status:  # Deployment events
  check_run, check_suite:  # Check events
  status:  # Commit status change
  label:  # Label modifications
```

<h3 style="color:#ff4b19">Jobs and Steps</h3>
Each workflow is composed of jobs, which run on specified virtual environments (like Ubuntu, Windows, or macOS). Jobs contain steps, which can include shell commands, actions, or scripts.

**Example Use Cases:**
- Continuous Integration: Automatically run tests and build your application whenever code is pushed to the repository.
- Continuous Deployment: Deploy code to production or staging environments after successful tests.
- Automated Code Quality Checks: Lint code or run static analysis on pull requests.
- Notifications: Send alerts or updates to team members based on repository events.

<h3 style="color:#ff4b19">Actions</h3> 

are reusable pieces of code that automate specific tasks within your workflows.

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

<h3 style="color:#ff4b19">Marketplace</h3> 

GitHub provides a marketplace where developers share their actions. You can find actions for common tasks, like deploying to cloud providers, sending notifications, or managing dependencies, and easily incorporate them into your workflows.

<h4 style="color:#ff4b19">Secrets Management:</h4> You can store sensitive information, like API keys and tokens, securely in GitHub Secrets and reference them in your workflows.

```yaml

password: $\{\{ secrets.secret_name \}\}

```

<h3 style="color:#ff4b19">Caching Techniques</h3> 

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

<h3 style="color:#ff4b19">Matrix Build</h3>

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

<h3 style="color:#ff4b19">Run multiple commands in a single Step</h3>

```yaml
steps:
  - name: Run multiple commands
    run: |
      echo "Step 1: Install dependencies"
      npm install
      echo "Step 2: Run tests"
      npm test
```

<h3 style="color:#ff4b19">Workflow that builds a Docker image and pushes it to a Docker registry</h3>

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

<h3 style="color:#ff4b19">Defining your own Action</h3>

```yaml
# .github/actions/my-action/new-action1.yaml
name: 'My Custom Action'
description: 'A brief description of what your action does.'
inputs:
  input1:
    description: 'Description of input1'
    required: true
    default: 'default-value'
outputs:
  output1:
    description: 'Description of output1'
runs:
  using: 'node12' # or 'docker' if you're using a Docker container
  steps:
    - name: "Invoke command with retries"
      shell: bash
      run: |
        set +e

        max_retries="${{ inputs.max-retries }}"
        count=0

        while (( count < max_retries )); do
          echo "Attempt $((count + 1)) of $max_retries..."
...

# .github/workflows/cicd.yml

uses: username/repo-name@branch
with:
  input1: 'value'

```

<h3 style="color:#ff4b19">Artifacts</h3>

An artifact is a file or collection of files produced during a workflow run. You can use actions such as actions/upload-artifact and actions/download-artifact to share artifacts between jobs or store them for use after workflows complete.

<h3 style="color:#ff4b19">Troubleshooting GitHub Actions Workflow</h3>

- Check the workflow logs: The workflow logs can provide you with information about the execution of your workflow.

- Use the GitHub Actions debug runner: The GitHub Actions debug runner allows you to run your workflow step by step and to inspect the environment variables and output of each step.

<h2 style="color:#ff4b19">Top 25 GitHub Commands</h2>

- git init: Initializes a new Git repository.
- git clone <repo>: Clones a remote repository to your local machine.
- git add <file>: Stages changes for the next commit.
- git add .: Stages all changes in the current directory.
- git commit -m "<message>": Commits staged changes with a message.
- git status: Displays the status of your working directory and staging area.
- git log: Shows the commit history for the repository.
- git diff: Shows changes between commits, working directory, etc.
- git branch: Lists all branches in the repository.
- git branch <branch-name>: Creates a new branch.
- git checkout <branch-name>: Switches to a specified branch.
- git checkout -b <branch-name>: Creates and switches to a new branch.
- git merge <branch-name>: Merges the specified branch into the current branch.
- git pull: Fetches changes from the remote repository and merges them.
- git push: Pushes local changes to the remote repository.
- git remote add <name> <url>: Adds a new remote repository.
- git remote -v: Lists the remote repositories.
- git fetch: Fetches changes from the remote repository without merging.
- git reset <file>: Unstages a file from the staging area.
- git reset --hard: Resets the working directory to match the latest commit (warning: this will discard changes).
- git cherry-pick <commit>: Applies the changes from a specific commit to the current branch.
- git stash: Temporarily saves changes that are not ready to be committed.
- git stash pop: Restores the most recent stashed changes.
- git rebase <branch>: Reapplies commits on top of another base branch.
- git tag <tag-name>: Creates a tag for a specific commit.


<h3 style="color:#ff4b19">Cherry-pick Commit</h3>

The git cherry-pick command uses exact commits from one branch to another, allowing selective merging of changes without merging entire branches.

<h3 style="color:#ff4b19">Large Files in Git</h3>

To handle large files in Git, use Git LFS (Large File Storage). It tracks large files severally from your repository, storing them on a remote server. This prevents bloating your repository size and secures improved performance while operations like cloning and fetching.
