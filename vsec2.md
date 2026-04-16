# Git Feature Branching, Merging, and Conflict Resolution

## Aim

To create feature branches, merge them, and resolve conflicts to
maintain separate workspaces for team collaboration.

------------------------------------------------------------------------

## Step 0: Repository Setup

``` bash
git init
git branch -M main
git remote add origin <repo-url>

echo "# Project" > README.md
git add README.md
git commit -m "Initial commit"
git push -u origin main
```

------------------------------------------------------------------------

## Step 1: Prepare Repository

``` bash
git checkout main
git pull origin main
git status
```

------------------------------------------------------------------------

## Step 2: Create First Feature Branch

``` bash
git checkout -b feature/branch-1
```

Create file:

``` bash
touch intro.txt
nano intro.txt
```

Add content:

    This is intro file from branch 1

``` bash
git add intro.txt
git commit -m "Add intro file in feature branch"
git push -u origin feature/branch-1
```

------------------------------------------------------------------------

## Step 3: Create Second Feature Branch

``` bash
git checkout main
git checkout -b feature/branch-2
```

Create file:

``` bash
touch notes.txt
nano notes.txt
```

Add content:

    This is notes file from branch 2

``` bash
git add notes.txt
git commit -m "Add notes file in second feature branch"
git push -u origin feature/branch-2
```

------------------------------------------------------------------------

## Step 4: Merge First Feature Branch

``` bash
git checkout main
git pull origin main
git merge feature/branch-1
git push origin main
```

------------------------------------------------------------------------

## Step 5: Create Conflict

On main branch:

``` bash
git checkout main
touch common.txt
nano common.txt
```

Add:

    This line is from MAIN branch.

``` bash
git add common.txt
git commit -m "Add common file in main"
git push origin main
```

On feature/branch-2:

``` bash
git checkout feature/branch-2
nano common.txt
```

Add:

    This line is from FEATURE BRANCH 2.

``` bash
git add common.txt
git commit -m "Modify common file in feature branch 2"
```

------------------------------------------------------------------------

## Step 6: Resolve Merge Conflict

``` bash
git checkout main
git merge feature/branch-2
```

Git will show conflict. Open file:

``` bash
nano common.txt
```

You will see:

    <<<<<<< HEAD
    This line is from MAIN branch.
    =======
    This line is from FEATURE BRANCH 2.
    >>>>>>> feature/branch-2

Edit to:

    This line is from MAIN branch.
    This line is from FEATURE BRANCH 2.

Then:

``` bash
git add common.txt
git commit -m "Resolve merge conflict"
git push origin main
```

------------------------------------------------------------------------

## Step 7: Cleanup Branches

``` bash
git branch -d feature/branch-1
git branch -d feature/branch-2

git push origin --delete feature/branch-1
git push origin --delete feature/branch-2
```

------------------------------------------------------------------------

## Output

Feature branches were created, merged successfully, and conflicts were
resolved, ensuring smooth collaboration.

------------------------------------------------------------------------

## Viva Points

-   Feature branches allow parallel development\
-   Merging integrates changes into main branch\
-   Conflicts occur when same file is modified\
-   Conflict markers must be manually resolved\
-   Git maintains version history

------------------------------------------------------------------------

## Memory Commands

``` bash
git checkout -b feature/branch
git add .
git commit -m "message"
git merge branch-name
git push
```
