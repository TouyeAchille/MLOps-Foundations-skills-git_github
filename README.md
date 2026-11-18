# Lab 1 – Create Your First Git Repository For Your Project On GitHub

In this first lab, you will create and configure the Git repository that you will use throughout this training series.

You will develop a small Python project focused on exploring and comparing three concurrency approaches:

- **Threading:** Running concurrent tasks using threads.
- **Multiprocessing:** Executing tasks in separate processes.
- **Asyncio:** Managing asynchronous operations using an event loop.

`Objective:` 

Throughout this project, you will learn essential Git and GitHub workflows, including repository initialization, git version control, branching, merging, committing, remote repository management, and collaboration.

By the end of this lab, you will have a structured, version-controlled Python project that serves as the foundation for the upcoming practical exercises.

## Prerequisites

- An account on GitHub. To sign up, go to <a href="https://github.com/signup"> github.com </a>
- uv tools. An extremely fast **Python package and project manager** <a href="https://docs.astral.sh/uv/getting-started/installation/"> installing uv </a>
- VS code
- tree
- GitHub CLI
- Git CLI

### 1. Creating your first repository for your project on GitHub

A repository is where you keep code and files for a software project on GitHub. It stores your files, tracks each change as a commit, and gives collaborators a shared place to work.

**Follow these steps to create your first repository :**
`
1 - In the upper-right corner of any page on GitHub, select `+`, then click `New repository`

2 - Create a GitHub repository named `python-concurrency-lab`, in the **Repository name** field, type `python-concurrency-lab`.

3 - In the **Description** field, type a short description, such as "A hands-on Python project exploring and benchmarking concurrency techniques using asyncio, threading, and multiprocessing. Learn how to execute concurrent tasks, compare performance, and understand Python's concurrency models."

4 - Use the `Choose visibility` dropdown menu to select **Public**. Visibility tells who can see and commit to this repository

5 - Select `Add README`. This gives your repository a starting file and a place to describe your software project.

6 - Select `Add .gitignore` and choose **Python** for python project.  Gitignore tells git which files not to track.

7 - Select `Add license`  and choose **MIT License**. Licenses explain how others can use your code

8 - Click `Create repository`.

### 2. Clone the remote repository to your local machine.

- Cloning with HTTPS URLs
The https:// clone URLs are available on all repositories, regardless of visibility.  When you `git clone`, `git fetch`, `git pull`, or `git push` to a **private remote repository** using `HTTPS URLs` on the command line, Git will ask for your `GitHub username and password`. When Git prompts you for your password, enter your `personal access token (PAT)`. For more information, see <a href="https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens"> Managing your personal access tokens.</a> 

Alternatively, you can use a credential helper like <a href="https://github.com/GitCredentialManager/git-credential-manager/blob/main/README.md"> Git Credential Manager.</a> You can use a credential helper so Git will remember your GitHub credentials every time it talks to GitHub. For more information, see <a href="https://docs.github.com/en/get-started/git-basics/caching-your-github-credentials-in-git"> Caching your GitHub credentials in Git. </a>

Tip

* To clone a repository without authenticating to GitHub on the command line, you can use `GitHub Desktop` to clone instead. For more information, see <a href="https://docs.github.com/en/desktop/adding-and-cloning-repositories/cloning-a-repository-from-github-to-github-desktop"> Cloning a repository from GitHub to GitHub Desktop.</a>

- Cloning with SSH URLs
SSH URLs provide access to a Git repository via SSH, a secure protocol. To use these URLs, you must generate an **SSH keypair on your computer and add the public key to your account on GitHub**. For more information, <a href='https://docs.github.com/en/authentication/connecting-to-github-with-ssh'> see Connecting to GitHub with SSH. </a>

When you git clone, git fetch, git pull, or git push to a remote repository using `SSH URLs`, you'll be prompted for a password and

Tip

* You can use an `SSH URL` to **clone a repository to your computer**, or as a secure way of **deploying your code to production servers**. 
* You can also use`SSH agent forwarding` with your **deploy script** to avoid managing keys on the server. For more information, see

On your local computer, type 

```bash
   git clone <YOUR_GITHUB_REMOTE_URL>
```

Then go to

```bash
   cd MLOps-Foundations-skills-git_github
```

- Cloning with GitHub CLI
You can also **install GitHub CLI** to use `GitHub workflows` in your terminal. For more information, <a href='https://docs.github.com/en/github-cli/github-cli/about-github-cli'>> see About GitHub CLI (gh). </a>


**Reference:**
- <a href='https://docs.github.com/en/repositories/creating-and-managing-repositories/cloning-a-repository'> cloning-a-repositories </a>
- <a href='<https://docs.github.com/en/get-started/git-basics/about-remote-repositories'> about-remote-repositories </a>


### 3. Create the project structure

Complete this step from the terminal in the local clone of your GitHub repository. The goal is to organize the Python package, documentation, automation, and test files shown below.

```text
.
├── .agents
│   └── skills                 # Custom AI or project-specific skills
├── .github
│   ├── actions
│   │   └── setup-venv
│   │       └── action.yml     # Reusable workflow for setting up the Python environment
│   └── workflows
│       ├── checkers.yml       # Runs code-formatting and static-checking jobs
│       ├── deploy-to-dev.yml  # Deploys the project to the development environment
│       └── tests.yml          # Runs automated tests in GitHub Actions
├── .gitignore                 # Lists local and generated files that Git must not track
├── .pre-commit-config.yaml    # Configures checks that run before each commit
├── .python-version            # Specifies the Python version used by the project
├── AGENTS.md                  # Provides instructions for AI coding assistants
├── docs                       # Stores project documentation
├── LICENSE                    # Defines how the project may be used and redistributed
├── Makefile                   # Defines shortcuts for common project commands
├── notebooks
│   └── experiments.ipynb      # Contains interactive experiments and analysis
├── pyproject.toml             # Defines project metadata, dependencies, and tool settings
├── README.md                  # Explains the project and provides setup instructions
├── src
│   └── mlops_git_github_skills_lab
│       ├── __init__.py        # Marks this folder as a Python package
│       ├── io
│       │   ├── __init__.py    # Marks the `io` directory as a Python subpackage
│       │   ├── asyncio_demo.py         # Demonstrates asynchronous concurrency
│       │   ├── multiprocessing_demo.py # Demonstrates process-based concurrency
│       │   └── threading_demo.py       # Demonstrates thread-based concurrency
│       └── scripts.py         # Contains reusable project scripts
├── tasks
│   ├── checkers.mk            # Defines code-checking Make tasks
│   ├── formatters.mk          # Defines code-formatting Make tasks
│   └── installers.mk          # Defines dependency-installation Make tasks
└── tests
    ├── integration_tests
    │   └── __init__.py        # Marks integration tests as a Python package
    ├── unit_tests
    │   └── __init__.py        # Marks unit tests as a Python package
    └── e2e_tests
        └── __init__.py        # Marks end-to-end tests as a Python package
```

#### 3.1 Initialize the Python package

Make sure the terminal is inside your cloned repository. Then run:

```bash
uv init --python 3.11 --package --name mlops_git_github_skills_lab .
```

This command creates the `pyproject.toml` file and the initial package under `src/mlops_git_github_skills_lab/`.

#### 3.2 Create the remaining directories

Use `mkdir` to create directories and `touch` to create empty files.

```bash
mkdir -p .agents/skills
mkdir -p .github/actions/setup-venv .github/workflows
mkdir -p docs notebooks tasks
mkdir -p src/mlops_git_github_skills_lab/io
mkdir -p tests/integration_tests tests/unit_tests tests/e2e_tests
```

#### 3.3 Create the project files

Create the automation, source, and test files named in the project structure:

```bash
touch .github/actions/setup-venv/action.yml
touch .github/workflows/checkers.yml
touch .github/workflows/deploy-to-dev.yml
touch .github/workflows/tests.yml
touch .pre-commit-config.yaml AGENTS.md Makefile
touch notebooks/experiments.ipynb
touch src/mlops_git_github_skills_lab/__init__.py
touch src/mlops_git_github_skills_lab/scripts.py
touch src/mlops_git_github_skills_lab/io/__init__.py
touch src/mlops_git_github_skills_lab/io/asyncio_demo.py
touch src/mlops_git_github_skills_lab/io/multiprocessing_demo.py
touch src/mlops_git_github_skills_lab/io/threading_demo.py
touch tasks/checkers.mk tasks/formatters.mk tasks/installers.mk
touch tests/integration_tests/__init__.py
touch tests/unit_tests/__init__.py
touch tests/e2e_tests/__init__.py
```

The `.gitignore`, `LICENSE`, `pyproject.toml`, and `README.md` files should already exist because you created them when setting up the GitHub repository and initializing the project.

#### 3.4 Verify the structure

Run the following command from the root of the repository:

```bash
tree .
```

Compare the output with the project structure shown at the beginning of Step 3. If a file or directory is missing, use the `mkdir` or `touch` command for that item.

### 4. Record your changes with Git

Git tracks the changes made to files in a project. A commit saves a selected set of changes as one clear, reviewable snapshot in the repository history.

#### 4.1 Check and select your changes

Run these commands from the root of the repository:

```bash
git status    # git-status - Show the working tree status
git diff
git add README.md
git status
```

| Command | What it does | When to use it |
|---|---|---|
| `git status` | Shows modified, deleted, and untracked files. | Check the project before and after staging. |
| `git diff` | Shows changes that are not staged yet. | Review edits before adding them. |
| `git add <file>` | Adds a file to the next commit. | Stage one file at a time for a focused commit. |
| `git add .` | Adds all changes in the repository. | Use only when every change belongs in the commit. |

#### 4.2 Write a clear commit message

Use this format:

```text
<type>(<scope>): <imperative description>
```

| Element | Rule | Example |
|---|---|---|
| `type` | Use a lowercase category that describes the change. | `feat`, `fix`, `docs` |
| `scope` | Optional, but useful when the change affects a specific area. | `readme`, `api`, `training` |
| `description` | Start with an imperative verb, such as `add`, `fix`, or `update`. | `add inference endpoint` |
| `subject length` | Keep it concise, ideally between 50 and 72 characters. | `docs(readme): update setup instructions` |
| `capitalization` | Capitalize only the first word when needed; do not use all capital letters. | `fix(api): validate request input` |
| `period` | Do not end the subject line with a period. | `test(api): add endpoint unit tests` |

#### 4.3 Choose the commit type

| Type | Use it when... | Example |
|---|---|---|
| `feat` | Adding a new feature or capability. | `feat(api): add inference endpoint` |
| `fix` | Correcting a bug or error. | `fix(auth): resolve token validation` |
| `docs` | Changing documentation only. | `docs(readme): update setup guide` |
| `style` | Formatting code without changing behavior. | `style: apply Ruff formatting` |
| `refactor` | Improving code structure without changing behavior. | `refactor(core): simplify model loader` |
| `perf` | Improving speed or resource usage. | `perf(inference): optimize batch processing` |
| `test` | Adding or updating tests. | `test(api): add endpoint unit tests` |
| `build` | Changing the build system or dependencies. | `build: update uv dependencies` |
| `ci` | Changing CI/CD configuration. | `ci(github): add testing workflow` |
| `chore` | Performing maintenance that does not fit another category. | `chore: update development tooling` |
| `revert` | Reverting an earlier commit. | `revert: remove broken inference endpoint` |

#### 4.4 Create the commit

Create one commit containing one logical change:

```bash
git commit -m "docs(readme): clarify project setup instructions"
```

If the commit needs more explanation, add a body:

```bash
git commit -m "docs(readme): clarify project setup instructions" \
  -m "Explain the required directories and add the purpose of each project file."
```

#### 4.5 Commit rules

| Rule | Correct example | Incorrect example |
|---|---|---|
| Use an imperative description. | `add inference endpoint` | `added inference endpoint` |
| Use a lowercase commit type. | `docs(readme): update guide` | `Docs(readme): update guide` |
| Keep the subject concise. | `fix(api): validate request input` | `fix(api): update and fix all API request validation problems` |
| Do not end with a period. | `test(api): add unit tests` | `test(api): add unit tests.` |
| Commit one logical change. | One README update | README, API, and test changes in the same commit |
| Explain why in the body when it is not obvious. | `Fixes incorrect validation...` | Only `fix: update code` |
| Use `!` for a breaking change. | `feat(api)!: replace v1 endpoint` | `feat(api): replace v1 endpoint` |

#### 4.6 Recommended MLOps and LLMOps scopes

| Scope | Area |
|---|---|
| `api` | REST API or FastAPI |
| `core` | Core application or shared business logic |
| `data` | Data processing and pipelines |
| `ml` | Machine learning |
| `dl` | Deep learning |
| `llm` | Large language models |
| `rag` | Retrieval-augmented generation |
| `agents` | AI agents |
| `training` | Model training |
| `inference` | Model prediction or generation |
| `evaluation` | Model and system evaluation |
| `monitoring` | Logs, metrics, and observability |
| `docker` | Containerization |
| `k8s` | Kubernetes |
| `github` | GitHub Actions and repository automation |
| `config` | Configuration files |
| `deps` | Dependencies |
| `security` | Security controls |

#### 4.7 Work with GitHub issues

| Convention | Purpose | Example |
|---|---|---|
| `Refs: #123` | References an issue or pull request without closing it. | `Refs: #123` |
| `Closes: #123` | Automatically closes issue `123` when the commit is merged. | `Closes: #123` |
| `BREAKING CHANGE:` | Describes an incompatible change. | `BREAKING CHANGE: Remove the v1 API endpoint` |

#### 4.8 Verify the commit

```bash
git log -1 --oneline
git status
```

`git log -1 --oneline` displays the latest commit. `git status` confirms whether the working tree still contains unstaged or untracked changes.


