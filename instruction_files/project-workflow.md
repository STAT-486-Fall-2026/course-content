# Setting Up a Reproducible Lab Project

This guide walks through a workflow for setting up a Python package for a lab, assignment, or small research-style project.

The goal is not just to make the code run once. The goal is to create a project that is:

- organized
- reproducible
- easy to test
- easy to revisit later
- easy to share through GitHub

In this course, a good project setup should make it easier to reason about machine learning work instead of fighting your tools.

## What this workflow is for

Use this workflow when you are:

- starting a new lab repository
- turning a rough folder of code into a clean package
- organizing a small research-style project
- preparing code that should be reproducible for grading or review

This guide connects several course tools and ideas:

- Git and GitHub for version control
- `uv` for Python environments and dependencies
- a clear folder structure for code, data, tests, and outputs
- a useful `README.md` so someone else can understand and rerun your work

If you want more detail about one tool, see the companion guides in this folder: `git.md`, `uv.md`, and `vscode.md`.

## The big picture

A good default workflow looks like this:

1. Create and open the project folder.
2. Initialize Git.
3. Add a `README.md`.
4. Create a clean project structure.
5. Set up the Python package with `uv`.
6. Add code, scripts, and tests.
7. Run the project through `uv`.
8. Commit meaningful progress.
9. Push the repository to GitHub.
10. Keep using the same repeatable workflow as the project evolves.

The key idea is consistency. If you follow the same structure each time, new labs/projects become much easier to set up and maintain.

## Step 1: Create or open the project folder

Start with a dedicated folder for the project.

Example:

```bash
mkdir lab-03-model-selection
cd lab-03-model-selection
```

Choose a folder name that is short, descriptive, and stable. Good project names usually:

- avoid spaces
- use lowercase letters
- use hyphens for the repository folder name
- reflect the lab or project theme

This outer folder will become the repository root. In a well-structured project, this is the folder that contains files such as:

- `.git/`
- `README.md`
- `pyproject.toml`
- `uv.lock`
- `src/`
- `scripts/`
- `tests/`

## Step 2: Initialize Git early

Initialize Git at the beginning, not at the end.

```bash
git init
git status
```

Why do this early:

- Git starts tracking your work from the beginning.
- You can commit the project structure before the code gets complicated.
- It is easier to recover from mistakes later.
- You build the habit of checking `git status` often.

If you already cloned a repository from GitHub, you do not need `git init` because the repository is already initialized.

## Step 3: Add a README right away

Create `README.md` near the beginning of the project, even if it is short at first.

A good project `README.md` should answer basic questions such as:

- What is this project?
- What is the goal of the lab?
- How do I set up the environment?
- How do I run the main workflow?
- Where do the answers or outputs go?

A short starting version is enough. You can improve it as the lab develops.

Useful early sections include:

- title
- short objective
- setup instructions
- run instructions
- file map
- short-answer or submission notes if the lab uses them

This is one of the best habits for reproducible work. A project that only makes sense in your memory is not yet well documented.

## Step 4: Create a clean project structure

Use a predictable layout so code, data, tests, and outputs do not get mixed together.

The course lab template uses this structure:

```text
project-root/
├── README.md
├── pyproject.toml
├── uv.lock
├── src/
│   └── your_package_name/
├── scripts/
├── tests/
├── data/
│   ├── sample/
│   └── raw/
└── results/
```

What each part is for:

- `README.md`
  Explains the project, setup, commands, and deliverables.
- `pyproject.toml`
  Defines the Python project and its dependencies.
- `uv.lock`
  Records the exact dependency resolution for reproducibility.
- `src/your_package_name/`
  Holds reusable Python code such as helpers, data-loading functions, models, and utilities.
- `scripts/`
  Holds runnable entrypoints such as `run.py` or `check.py`.
- `tests/`
  Holds smoke tests or small checks that confirm the project works.
- `data/sample/`
  Holds tiny tracked example data.
- `data/raw/`
  Holds larger or lab-specific raw data that usually should not be committed.
- `results/`
  Holds generated outputs that can be reproduced from the code.

This separation matters. Reusable code should not be buried inside one giant script, and generated outputs should not be mixed into the source package.

## Step 5: Set up the package with uv

In this course, `uv` is the standard tool for Python project setup.

If you are creating a brand-new project from scratch, initialize the project metadata first:

```bash
uv init
```

If you are working in a course repository that already includes `pyproject.toml`, you will usually start with:

```bash
uv sync
```

What to expect:

- `pyproject.toml` describes the package and dependencies.
- `uv sync` creates or updates the project environment.
- `uv run ...` runs commands inside that environment.

Common examples:

```bash
uv sync
uv run python --version
uv run python scripts/run.py
uv run pytest
```

Best practice:

- do not install course dependencies globally if the repository is already managed by `uv`
- do not mix random `pip install` commands into a project unless you have a good reason
- treat the project configuration as the source of truth

If you need more background, see `uv.md`.

## Step 6: Add package code, scripts, and tests

Once the environment exists, start placing work in the right folders.

### Code in `src/`

Put reusable logic in `src/your_package_name/`.

Examples:

- data loading functions
- preprocessing helpers
- model utilities
- evaluation helpers
- plotting helpers

This makes the project easier to test and easier to reuse from multiple scripts.

### Entry points in `scripts/`

Put top-level runnable workflows in `scripts/`.

Examples:

- `scripts/run.py`
- `scripts/check.py`
- `scripts/make_figures.py`

The script should usually call functions from the package instead of containing all logic directly.

### Tests in `tests/`

Put smoke tests or small correctness checks in `tests/`.

Examples:

- can the sample data be loaded?
- does the main script run?
- does a key helper function return the right shape or type?

In many course projects, even a very small test suite is much better than none.

## Step 7: Decide what belongs in version control

Not every file in the folder should be committed.

Good things to track:

- source code
- `README.md`
- `pyproject.toml`
- `uv.lock`
- small sample data
- tests
- lightweight configuration files

Usually avoid committing:

- `.venv/`
- cache folders
- temporary files
- editor-specific clutter
- large raw datasets
- outputs that can be regenerated easily, unless the instructor wants them tracked

This is why a `.gitignore` file matters. It helps prevent accidental commits of messy or irrelevant files.

Typical examples to ignore:

```text
.venv/
__pycache__/
.pytest_cache/
data/raw/
```

If you are unsure whether a file belongs in the repository, check before pushing.

## Step 8: Understand when to use uv lock

`uv.lock` is important for reproducibility because it captures the resolved dependency set.

In this course, students will often receive a repository that already contains `uv.lock`. In that case:

- keep the lockfile in the repository
- use `uv sync` to respect the shared environment
- avoid changing dependencies unless the lab instructions tell you to

When you are building or updating a project yourself, use:

```bash
uv lock
```

Common times to update the lockfile:

- after adding a new dependency
- after removing a dependency
- after changing version constraints in `pyproject.toml`

If nothing about the dependencies changed, you usually do not need to regenerate the lockfile just because you ran the project.

## Step 9: Make the first clean commit

After the structure and basic files are in place, create an early commit.

Typical workflow:

```bash
git status
git add .
git commit -m "Set up initial lab package structure"
```

Why commit early:

- you create a restore point
- you can separate setup work from later analysis work
- your project history becomes easier to understand

Good commit messages are short but meaningful. A reader should be able to tell what changed without guessing.

Better examples:

- `Set up initial lab package structure`
- `Add sample data loader and run script`
- `Write smoke tests for setup workflow`

Less helpful examples:

- `stuff`
- `update`
- `changes`

## Step 10: Connect the project to GitHub

Once the repository is in good shape locally, connect it to GitHub.

If you are starting from a local repository, a common workflow is:

```bash
git remote add origin <repository-url>
git branch -M main
git push -u origin main
```

If the repository already exists on GitHub and you cloned it first, then the remote is already set up and you can usually just push after committing.

Why GitHub matters here:

- it backs up your work
- it gives the instructor or teammates a clear source of truth
- it makes submission and review easier
- it encourages a clean version-control workflow

If you need more detail about Git commands or GitHub usage, see `git.md`.

## Step 11: Follow the day-to-day project loop

After setup, the normal workflow should be simple and repeatable.

For most labs, the loop looks like this:

1. Open the repository folder.
2. Run `uv sync` if needed.
3. Work on code or answers.
4. Run the main script with `uv run ...`.
5. Run tests.
6. Check `git status`.
7. Commit meaningful progress.
8. Push to GitHub.

Example:

```bash
uv sync
uv run python scripts/run.py
uv run pytest
git status
git add .
git commit -m "Finish baseline analysis workflow"
git push
```

This repeatable loop is one of the main goals of the whole setup.

## A principled README workflow

A good `README.md` should grow with the project.

At minimum, it should usually include:

- project title
- short description or objective
- setup steps
- run commands
- file map
- explanation of where answers or outputs belong

For many lab repositories, the `README.md` is also the best place for:

- short written responses
- notes about expected outputs
- reproducibility instructions
- submission checklist items

You do not need a long essay. You do need enough information that another student, instructor, or future version of you can understand how to rerun the project.

## Best practices that matter most

If you remember only a few habits, remember these:

- Open the repository root, not just one file.
- Initialize Git early or clone the repository before you begin working.
- Keep code, data, tests, and outputs in separate places.
- Use `uv sync` and `uv run ...` instead of mixing environments.
- Commit small, meaningful chunks of progress.
- Keep `README.md` current.
- Do not commit virtual environments, caches, or large raw data by accident.
- Prefer reproducible scripts and functions over one-off manual steps.

These habits make labs easier to debug, easier to grade, and easier to extend into larger research work later.

## Common mistakes to avoid

### Putting everything in one notebook or one script

This often makes code hard to test, hard to reuse, and hard to debug.

A better pattern is:

- reusable logic in `src/`
- runnable workflows in `scripts/`
- explanation in `README.md`

### Running plain `python` instead of `uv run python`

This can accidentally use the wrong interpreter or the wrong installed packages.

When the project uses `uv`, prefer:

```bash
uv run python scripts/run.py
```

### Forgetting to check `git status`

Students often commit too much, too little, or the wrong files because they skip `git status`.

Use it often.

### Tracking files that should stay local

Examples:

- `.venv/`
- cache directories
- temporary notebooks or exports
- large raw datasets

These files usually create noise and confusion in the repository.

### Writing no README or an empty README

If someone cannot tell how to run the project, the project is not yet fully reproducible.

## A simple starter command sequence

For a new local project, a basic setup might look like this:

```bash
mkdir my-lab-project
cd my-lab-project
git init
uv init
uv sync
git status
git add .
git commit -m "Set up project scaffold"
```

For a course lab repository that already exists, a basic working session might look like this:

```bash
git clone <repository-url>
cd <repository-folder>
uv sync
uv run python scripts/run.py
uv run pytest
git status
git add .
git commit -m "Complete lab work"
git push
```

## When to ask for help

Ask for help early if project setup starts blocking your work. When you ask, include:

- operating system
- Python version
- `uv` version
- exact commands you ran
- full error messages as text
- current `git status`
- what you already tried

That information makes it much easier for someone to help you quickly.
