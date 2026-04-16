# Fork an Open-Source AI Project and Submit a Pull Request

## Aim

To fork an open-source AI project, make a contribution, and submit a
pull request to collaborate with the original repository.

------------------------------------------------------------------------

## Step 1: Fork Open-Source Repository

1.  Go to GitHub
2.  Search: awesome-machine-learning
3.  Open repository by josephmisiti
4.  Click **Fork** (top-right)
5.  Repository will be copied to your GitHub account

------------------------------------------------------------------------

## Step 2: Clone Fork & Setup Upstream

``` bash
git clone https://github.com/<your-username>/awesome-machine-learning.git
cd awesome-machine-learning

git remote add upstream https://github.com/josephmisiti/awesome-machine-learning.git
git remote -v
```

------------------------------------------------------------------------

## Step 3: Create Feature Branch

``` bash
git checkout master
git pull upstream master
git checkout -b feature/add-ai-resource
```

------------------------------------------------------------------------

## Step 4: Make Contribution

Edit README.md:

``` bash
nano README.md
```

Add this line anywhere appropriate:

    - **Machine Learning Mastery** – Practical tutorials for machine learning and deep learning.

Save file.

``` bash
git add README.md
git commit -m "Add machine learning resource"
git push -u origin feature/add-ai-resource
```

------------------------------------------------------------------------

## Step 5: Create Pull Request (GitHub)

1.  Go to your forked repository on GitHub
2.  Click **Compare & Pull Request**
3.  Check:
    -   Base repo: josephmisiti/awesome-machine-learning
    -   Base branch: master
    -   Head repo: your fork
    -   Compare branch: feature/add-ai-resource
4.  Click **Create Pull Request**

------------------------------------------------------------------------

## Step 6: Handle Merge Conflicts (If Any)

``` bash
git fetch upstream
git checkout feature/add-ai-resource
git merge upstream/master
```

If conflict occurs:

Open file:

``` bash
nano README.md
```

You will see markers:

    <<<<<<< HEAD
    =======
    >>>>>>>

Fix manually by keeping correct content.

Then:

``` bash
git add README.md
git commit -m "Resolve merge conflict with upstream"
git push origin feature/add-ai-resource
```

------------------------------------------------------------------------

## If No Conflict

Git may show:

    Already up to date.

This means everything is correct.

------------------------------------------------------------------------

## Output

Successfully forked repository, created feature branch, added
contribution, and submitted pull request.

------------------------------------------------------------------------

## Viva Points

-   Fork creates copy of repository\
-   Upstream links original repo\
-   Feature branches isolate changes\
-   Pull Requests enable collaboration\
-   Conflicts occur when same lines are modified\
-   Conflict resolution is manual

------------------------------------------------------------------------

## Memory Commands

``` bash
git clone <repo>
git checkout -b feature/name
git add .
git commit -m "message"
git push origin branch
```
