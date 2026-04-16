# Git Repository Setup for Data Science Project

## Aim

To set up a Git repository for a data science project and push it to
GitHub for version control and tracking changes.

------------------------------------------------------------------------

## Step 1: Install Git (Ubuntu)

``` bash
sudo apt update
sudo apt install git -y
```

Verify installation:

``` bash
git --version
```

------------------------------------------------------------------------

## Step 2: Configure Git (First Time Only)

``` bash
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

Check config:

``` bash
git config --list
```

------------------------------------------------------------------------

## Step 3: Create Project Folder

``` bash
mkdir my-data-science-project
cd my-data-science-project
```

------------------------------------------------------------------------

## Step 4: Create Sample Project Files

``` bash
touch main.py
touch README.md
```

Add simple code:

``` bash
nano main.py
```

Paste:

``` python
print("Hello Data Science Project")
```

Save: Ctrl + X → Y → Enter

------------------------------------------------------------------------

## Step 5: Initialize Git Repository

``` bash
git init
```

------------------------------------------------------------------------

## Step 6: Check Status

``` bash
git status
```

------------------------------------------------------------------------

## Step 7: Add Files to Git

``` bash
git add .
```

------------------------------------------------------------------------

## Step 8: Commit Files

``` bash
git commit -m "Initial commit"
```

------------------------------------------------------------------------

## Step 9: Create GitHub Repository

1.  Go to: https://github.com
2.  Click "New Repository"
3.  Enter name: my-data-science-project
4.  Do NOT add README (important)
5.  Click "Create Repository"

------------------------------------------------------------------------

## Step 10: Connect Local Repo to GitHub

Copy your repo URL and run:

``` bash
git remote add origin https://github.com/your-username/my-data-science-project.git
```

------------------------------------------------------------------------

## Step 11: Push Code to GitHub

``` bash
git branch -M main
git push -u origin main
```

------------------------------------------------------------------------

## Step 12: Verify

Open your GitHub repository in browser\
→ Files should be visible

------------------------------------------------------------------------

## Output

The Git repository was successfully created, managed locally, and pushed
to GitHub for version control and collaboration.

------------------------------------------------------------------------

## Viva Points

-   Git is used for version control\
-   GitHub is used for remote repository hosting\
-   `git init` initializes repository\
-   `git add` stages changes\
-   `git commit` saves changes\
-   `git push` uploads to GitHub

------------------------------------------------------------------------

## Memory Commands

``` bash
git init
git add .
git commit -m "Initial commit"
git remote add origin <repo_url>
git push -u origin main
```
