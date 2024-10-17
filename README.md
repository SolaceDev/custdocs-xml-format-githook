
# How to Set Up the `xmllint` Pre-Commit Hook

This guide explains how to set up a pre-commit hook to automatically format `.xml`, `.html`, and `.htm` files using the `xmllint` tool. Pre-commit hooks ensure files are formatted correctly before being committed to version control, maintaining consistency across your repository.

## What is `xmllint`?
`xmllint` is a command-line tool for validating and formatting XML files. It ensures files are formatted correctly according to standard XML conventions. In this guide, we'll integrate `xmllint` into a pre-commit hook to automatically format `.xml`, `.html`, and `.htm` files.

---

## Pre-Commit Hook Overview

1. **`format-xmllint`:**
   - Formats `.xml`, `.html`, and `.htm` files using `xmllint --format`.
   - Overwrites the files if they are not properly formatted.

2. **`check-xmllint`:**
   - Checks if the files are formatted according to `xmllint --format`.
   - **Note:** We recommend using `format-xmllint`, as `check-xmllint` only verifies formatting without fixing it.

---

## Step 1: Install Pre-Commit

Before setting up the hook, you'll need to install the `pre-commit` tool. Here's how to install it on different environments:

### Installing Pre-Commit

#### On macOS:
1. Open your terminal.
2. Install `pre-commit` using Homebrew:

   ```bash
   brew install pre-commit
   ```

3. Verify the installation:

   ```bash
   pre-commit --version
   ```

#### On Linux:
1. Open your terminal.
2. Install `pre-commit` using pip (Python package manager):

   ```bash
   pip install pre-commit
   ```

3. Verify the installation:

   ```bash
   pre-commit --version
   ```

4. On some distributions, you may need to install additional dependencies:

   ```bash
   sudo apt install python3-pip
   ```

#### On Windows:
1. If you don't have Python installed, download and install [Python](https://www.python.org/downloads/), which comes with pip.
2. Open PowerShell or Command Prompt.
3. Install `pre-commit` using pip:

   ```bash
   pip install pre-commit
   ```

4. Verify the installation:

   ```bash
   pre-commit --version
   ```

#### Using Docker:
If you prefer Docker, you can run `pre-commit` in a Docker container:

```bash
docker run --rm -v $(pwd):/repo pre-commit run --all-files
```

---

## Step 2: Install `xmllint`

Ensure that `xmllint` is installed on your system. Here’s how to install it on different operating systems:

#### On macOS (via Homebrew):
```bash
brew install libxml2
```

#### On Linux:
```bash
sudo apt install libxml2-utils
```

#### On Windows:
You can use **Windows Subsystem for Linux (WSL)** or a package manager like **Cygwin** to install `xmllint`. In WSL, run:

```bash
sudo apt install libxml2-utils
```

Verify that `xmllint` is available by running:

```bash
xmllint --version
```

---

## Step 3: Create or Update the `.pre-commit-config.yaml`

In the root directory of your repository, create or update a `.pre-commit-config.yaml` file with the following configuration:

```yaml
repos:
  - repo: https://github.com/Patrick-Bonini/xml-format-githook
    rev: v1.0.1
    hooks:
      - id: format-xmllint
```

### Explanation:
- **`repo:`** The repository URL hosting the pre-commit hook.
- **`rev:`** The version of the hook to use (`v1.0.1` in this example).
- **`id:`** The identifier for the hook (`format-xmllint`).
- **`files:`** The regex pattern that specifies which file types the hook should target (`.xml`, `.html`, and `.htm`).

---

## Step 4: Install the Pre-Commit Hook

After configuring the `.pre-commit-config.yaml` file, install the pre-commit hook by running:

```bash
pre-commit install
```

This will ensure that every time you make a commit, the hook will check and format any `.xml`, `.html`, and `.htm` files before committing them.

---

## Step 5: Running the Hook

You can manually trigger the pre-commit hook to check and format all files in your repository by running:

```bash
pre-commit run --all-files
```

---

### What Happens During a Commit?

- When you attempt to commit files, the hook will automatically run and check the formatting of any `.xml`, `.html`, or `.htm` files.
- If the files are not properly formatted, `format-xmllint` will reformat them, and you’ll need to stage the corrected files and commit again.
- This process ensures that your repository maintains consistent and correct formatting.

---

## Troubleshooting

- **`xmllint` not found**: Ensure that `xmllint` is installed and accessible via your command line.
- **Hook not running on `.html` or `.htm` files**: Double-check that your `.pre-commit-config.yaml` file is correctly targeting the file extensions.
- **Permission errors**: Make sure the `check-xmllint` script is executable by running:

  ```bash
  chmod +x check-xmllint
  ```

---

## Conclusion

By setting up the `xmllint` pre-commit hook, you ensure that your `.xml`, `.html`, and `.htm` files are always formatted correctly before they are committed. This automated process helps maintain code quality, consistency, and readability across your project.

For further assistance or questions, feel free to reach out to your development team or consult the pre-commit documentation.
