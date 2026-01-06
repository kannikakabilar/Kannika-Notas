<h1 style="color:#ff4b19">GitHub Actions</h1> 

A CI/CD service provided by GitHub that allows you to automate workflows directly within your GitHub repositories.

<h3 style="color:#ff4b19">Workflows</h3>
Defined workflows in YAML files stored in the .github/workflows directory of your repository. Each workflow can consist of multiple jobs that can run sequentially or in parallel.

<h2 style="color:#ff4b19">Triggers</h2>
Workflows can be triggered by various GitHub events, such as push, pull requests, and more. It can also run on schedule workflows or via API calls.

<h3 style="color:#ff4b19">Triggers - Basic</h3>

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
```

<h3 style="color:#ff4b19">Triggers - pull_request</h3>

```yaml
name: PR Workflow

on:  
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
```

<h3 style="color:#ff4b19">Triggers - workflow_call vs workflow_run</h3>

```yaml
name: Random Workflow

on:
  workflow_call:  # Makes the workflow reusable (can be called by other workflows)
    inputs:
      nameOfInput1:
        description: "Please enter input1 value"
        required: true
        default: 1
        type: number
  workflow_run:  # Triggers when the listed workflow runs
    workflows:
      - "Package and release"
      - "(Single-card) Frequent model and ttnn tests"
```

<h3 style="color:#ff4b19">Use workflow_call to make the workflow reusable</h3>

```yaml
# Calling a workflow that has workflow_call: in it
name: "Wrapper workflow"

on:
  workflow_dispatch:
    inputs:
      requested-models:
        description: "List of requested models as JSON array, for example: [\"resnet\", \"sdxl\"]. Default is 'all'"
        default: "all"
        type: string
      run-perf-tests:
        description: "Run perf variants"
        type: boolean
        default: true
      enable-ops-recording:
        description: "Enable Tracy ops recording for all tests (generates operations report)"
        type: boolean
        default: false
  schedule:
    - cron: "0 13,18 * * 0,1,2,3,4,5,6" # frequency of functional models
    - cron: "0 5 * * 1,3,6" # frequency of perf models

run-name: "(Single-card) Demo tests${{ (inputs.run-perf-tests || (github.event_name != 'workflow_dispatch' && github.event.schedule == '0 5 * * 1,3,6')) && ' (with perf runs)' || ' (no perf)' }}${{ inputs.enable-ops-recording && ' [ops-recording]' || '' }}"
jobs:
  build-artifact:
    uses: ./.github/workflows/build-artifact.yaml  # Only 1 reusable workflow per job and each 'uses:' can only reference a single workflow file
    permissions:
      packages: write  # Overrides workflow-level permission because workflow-level permissions are always ignored
    secrets: inherit  # this line allows the reusable workflow to have access to the repo secrets
    with:
      build-wheel: true
      version: 22.04
      tracy: ${{ inputs.enable-ops-recording || false }}

  # Calling the reusable workflow and enter the required inputs under 'with:' section
  single-card-demo-tests:
    needs: build-artifact
    secrets: inherit
    uses: ./.github/workflows/single-card-demo-tests-impl.yaml
    with:
      docker-image: ${{ needs.build-artifact.outputs.dev-docker-image }}  # The outputs defined in the build-artifact workflow can be used to input here
      build-artifact-name: ${{ needs.build-artifact.outputs.build-artifact-name }}
      wheel-artifact-name: ${{ needs.build-artifact.outputs.wheel-artifact-name }}
      arch: wormhole_b0
      requested-models: ${{ inputs.requested-models || 'all' }}
      # Using || true after is dangerous since that will always be passed in if first value is falsy
      run-perf-tests: ${{ inputs.run-perf-tests || (github.event_name != 'workflow_dispatch' && github.event.schedule == '0 5 * * 1,3,6') }}
      enable-ops-recording: ${{ inputs.enable-ops-recording || false }}
```

<h3 style="color:#ff4b19">Triggers - API Call</h3>

```yaml
name: Workflow Triggered by API Call

on:
  repository_dispatch:  # is a webhook-based trigger that allows you to remotely trigger a workflow via a GitHub API
    types: [trigger-llk-update]
    # And this is how you can trigger the workflow - You send a POST request to GitHub's API with a custom event type 
    # which has to be trigger-llk-update and any other event type trigger won't work
    # curl -X POST \
    #   -H "Accept: application/vnd.github+json" \
    #   -H "Authorization: Bearer YOUR_TOKEN" \
    #   https://api.github.com/repos/OWNER/REPO/dispatches \
    #   -d '{"event_type":"trigger-llk-update","client_payload":{"key":"value"}}'
```

<h3 style="color:#ff4b19">Triggers - Merge Queue</h3>

```yaml
name: Workflow running in Merge Queue

on:
  merge_group:  # Runs on merge queue events
    types:
      - checks_requested  # When PR enters or moves in the merge queue (The workflow runs tests on tmp commit with the merged code PR+main+any_PRs_queued_above)
      - destroyed  # When the PR leaves the merge queue
```

<h3 style="color:#ff4b19">Triggers - Other</h3>

```yaml
name: Other Workflow Triggers

on:
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

<h2 style="color:#ff4b19">Inputs</h2>
Inputs can be checkbox, text field, number, dropdown (that only allows one selected choice)

```yaml
name: "Nightly tt-metal L2 tests"

on:
  schedule:
    - cron: "0 6 * * *"
  workflow_dispatch:
    inputs:
      run_didt_tests:
        description: 'Run DIDT tests'
        required: false
        type: boolean
        default: false
      additional_test_categories:
        description: 'Additional test categories to run (comma-separated, e.g., conv,pool,sdxl,eltwise,matmul,moreh,fused,data_movement,transformers)'
        required: false
        type: string
        default: ''
      timeout:
        description: 'Test timeout in minutes'
        required: false
        type: number
        default: 150
      environment:
        type: choice  # to have dropdown for inputs but only one option can be selected
        description: 'Target environment'
        options:
          - development
          - staging
          - production
        default: development
```

<h2 style="color:#ff4b19">Outputs</h2>

Outputs can pass data between steps, jobs, and workflows

Step Output => Job Output => Another Job

<h3 style="color:#ff4b19">Job-level Outputs</h3>

```yaml
jobs:
  my-job1:
    runs-on: ubuntu-latest
    outputs:
      # Define job outputs (what other jobs can access)
      my-value: ${{ steps.step1.outputs.result }}
      version: ${{ steps.calculate.outputs.version }}
    steps:
      - name: Calculate result
        id: step1  # MUST have an id to reference later
        run: |
          echo "result=hello-world" >> $GITHUB_OUTPUT

      - name: Calculate version
        id: calculate
        run: |
          VERSION="v1.2.3"
          echo "version=$VERSION" >> $GITHUB_OUTPUT

  my-job2:
    needs: my-job1 # MUST include the needs to indicate this job will run once job1 finishes and produces the output
    runs-on: ubuntu-latest
    steps:
      - name: Use the outputs
        run: |
          echo "Got value: ${{ needs.my-job1.outputs.my-value }}
          echo "Got version: ${{ needs.my-job1.outputs.version }}
```

<h3 style="color:#ff4b19">Workflow-level Outputs</h3>

```yaml
# The reusable workflow
on:
  workflow_call:
    outputs:
      # Define what outputs this workflow returns
      docker-tag:
        description: "The Docker image tag"
        value: ${{ jobs.build.outputs.tag }}
      artifact-name:
        description: "Name of the Artifact"
        value: ${{ jobs.build.outputs.artifact }}

jobs:
  build:
    runs-on: ubuntu-latest
    outputs:
      tag: ${{ steps.build-image.outputs.image-tag }}
      artifact: ${{ steps.create.outputs.name }}
    steps:
      - id: build-image
        run: echo "image-tag=myapp:v1.0" >> $GITHUB_OUTPUT

      - id: create
        run: echo "name=my-artifact-123" >> $GITHUB_OUTPUT

#----------------------------------------------------------------#

# Calling workflow

jobs:
  build:
    uses: ./github/workflows/reusable-workflow.yaml

  test:
    needs: build
    runs-on: ubuntu-latest
    steps:
      - run: echo "Using image: ${{ needs.build.outputs.docker-tag }}"
      - run: echo "Using artifact: ${{ needs.build.outputs.artifact-name }}"
```

<h2 style="color:#ff4b19">Jobs and Steps</h2>

Each workflow is composed of jobs, which run on specified virtual environments (like Ubuntu, Windows, or macOS). Jobs contain steps, which can include shell commands, actions, or scripts.

**Example Use Cases:**
- Continuous Integration: Automatically run tests and build your application whenever code is pushed to the repository.
- Continuous Deployment: Deploy code to production or staging environments after successful tests.
- Automated Code Quality Checks: Lint code or run static analysis on pull requests.
- Notifications: Send alerts or updates to team members based on repository events.

<h3 style="color:#ff4b19">Run multiple commands in a single run: arg</h3>

```yaml
steps:
  - name: Run multiple commands
    run: |
      echo "Step 1: Install dependencies"
      npm install
      echo "Step 2: Run tests"
      npm test
```

<h2 style="color:#ff4b19">Matrix Strategies</h2>

<h3 style="color:#ff4b19">Matrix Build</h3>
It allows you to run multiple versions of your job in parallel like in different OS or different ML model tests.

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

<h3 style="color:#ff4b19">Handling edge-cases with include and exclude</h3>

```yaml
... # Include
strategy:
  matrix:
    test_type: [conv, pool, group_norm]
    include:
      - test_type: conv
        test_path: tests/ttnn/nightly/conv
        owner: U052J2QDDKQ  # Pavle
      - test_type: pool
        test_path: tests/ttnn/nightly/pool
        owner: U052J2QDDKR  # Evan
      - test_type: group_norm
        test_path: tests/ttnn/nightly/group_norm
        owner: U052J2QDDKS  # Borys

... # Exclude
strategy:
  fail-fast: false  # if one job fails in the matrix, don't fail fast and continue to the next job
  matrix:
    os: [ubuntu-latest, windows-latest, macos-latest]
    node: [14, 16, 18, 20]
    exclude:
      # Node 14 is not supported on Windows
      - os: windows-latest
        node: 14
      # Node 16 has issues on MacOS
      - os: macos-latest
        node: 16
```

<h3 style="color:#ff4b19">Concurrency Group</h3>

Think of a concurrency group as a unique "slot." When you assign a workflow or a job to a group name, GitHub ensures that only one process with that specific name runs at a time.

If a new workflow starts and another one with the same group name is already running, the new one will be "pending" until the first one finishes.

The **cancel-in-progress** feature is an optional setting within a concurrency group. It allows you to tell GitHub: "If a new version of this workflow starts, kill the old one immediately and focus on the latest one."

Example

```yaml
name: Deployment
on: [push]

# This is the concurrency configuration
concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}  # The name of the workflow - The specific branch or tag
  # This ensures that pushing to the feature-a branch only cancels other runs on feature-a, without affecting runs happening on the main branch
  cancel-in-progress: true

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - title: Deploying code...
        run: sleep 60 # Simulating a long task
```

<h2 style="color:#ff4b19">Containerized Jobs</h2>

To "containerize" a job in GitHub Actions means you want the entire job to run inside a specific Docker container rather than directly on the runner's host machine (the virtual machine). This is incredibly useful because it guarantees that your tools, OS versions, and environment variables are identical every time, regardless of what's installed on the GitHub-hosted runner.


```yaml
# Basic example
jobs:
  my_job_name:
    runs-on: ubuntu-latest
    # This tells GitHub to start the container, and run every step of this job inside the container
    container:
      image: node:18-bookworm
    
    steps:
      - uses: actions/checkout@v4
      - run: node --version # This runs inside the 'node:18' container
# ----------------------------------------------------------------------------------------------------

# Advanced example
jobs:
  build:
    runs-on: ubuntu-latest
    container:
      image: ghcr.io/my-org/my-custom-image:latest
      # Provide credentials for private registries
      credentials:
        username: ${{ github.actor }}
        password: ${{ secrets.GITHUB_TOKEN }}
      # Pass environment variables to the container
      env:
        NODE_ENV: production
      # Map ports or volumes
      ports:
        - 8080:80
      volumes:
        - my_docker_volume:/volume_mount
      # Add standard Docker 'run' options
      options: --cpus 1 --user root
    
    steps:
      - run: whoami
```

<h3 style="color:#ff4b19">Key things to know about containerization</h3>

**Linux Only:** Container jobs only work on Linux runners (ubuntu-latest, etc.). They are not supported on Windows or macOS runners.

**Default Shell:** Inside a container, the default shell is often sh rather than bash. If your scripts rely on "bashisms" (like [[ ]]), you should explicitly set the shell:

```yaml
defaults:
  run:
    shell: bash
```

<h3 style="color:#ff4b19">Service Containers</h3>

To run a database or a cache alongside your containerized job, you use Service Containers. These are "sidecar" containers that start before your job begins and are destroyed when the job finishes.

When you define a services block, GitHub creates a network and connects both your main job container and the service containers to it. This allows your code to communicate with the service using its ID as the hostname.

```yaml
jobs:
  test-database:
    runs-on: ubuntu-latest
    # Main container where your code runs
    container:
      image: node:18-bookworm

    # Service containers running in the background
    # Networking: If your job runs in a container, you connect to services using the service name (e.g., postgres or redis). If your job runs directly on the host (runs-on: ubuntu-latest without a container block), you connect via localhost:<mapped-port>.
    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: password
        # Wait for postgres to be "healthy" before starting the job
        # Health Checks: It's a best practice to use the options key to include a health check. This ensures your code doesn't start running before the database is fully booted up.
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - uses: actions/checkout@v4
      - name: Connect to Database
        run: |
          # Use 'postgres' as the hostname
          npm install pg
          node -e "const { Client } = require('pg'); const c = new Client('postgresql://postgres:password@postgres:5432'); c.connect().then(() => console.log('Connected!'))"
```

<h2 style="color:#ff4b19">Actions</h2>

Actions are reusable pieces of code that automate specific tasks within your workflows. The actions are defines somewhere in GitHub's original repo?

```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Run Tests
        uses: my-org/run-tests@v1  # This is your reusable action called Composite Action
```

<h3 style="color:#ff4b19">Composite Action</h3>

You can define your own action in the actions sub-folder under .github

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

<h3 style="color:#ff4b19">Composite Actions vs Reusable Workflows</h3>

- reuse a sequence of steps -> composite actions
- light weight operations -> composite actions
- different runner requirements -> reusable workflow
- matrix strategy -> reusable workflow
