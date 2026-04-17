# Jenkins Build Trigger using Local Git (Ultra Noob Version)

## Aim

To configure Jenkins to access a local project folder and automatically
trigger builds when code is updated using Git from the terminal.

------------------------------------------------------------------------

## Requirements

-   Ubuntu system\
-   Internet (only for installation)\
-   Basic terminal usage

------------------------------------------------------------------------

## Step 1: Install Java (Required for Jenkins)

``` bash
sudo apt update
sudo apt install openjdk-11-jdk -y
```

Verify:

``` bash
java -version
```

------------------------------------------------------------------------

## Step 2: Install Jenkins

``` bash
sudo apt install jenkins -y
```

------------------------------------------------------------------------

## Step 3: Start Jenkins Service

``` bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Check:

``` bash
sudo systemctl status jenkins
```

------------------------------------------------------------------------

## Step 4: Open Jenkins

http://localhost:8080

------------------------------------------------------------------------

## Step 5: Unlock Jenkins

``` bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste password → Install Suggested Plugins

------------------------------------------------------------------------

## Step 6: Install Git

``` bash
sudo apt install git -y
git --version
```

------------------------------------------------------------------------

## Step 7: Create Project Folder

``` bash
mkdir ~/jenkins-local-project
cd ~/jenkins-local-project
pwd
```

------------------------------------------------------------------------

## Step 8: Create Python File

``` bash
nano app.py
```

Paste:

``` python
print("Hello from Jenkins Build")
```

------------------------------------------------------------------------

## Step 9: Initialize Git

``` bash
git init
git add .
git commit -m "Initial commit"
```

------------------------------------------------------------------------

## Step 10: Fix Permissions

``` bash
sudo chmod -R 777 ~/jenkins-local-project
```

------------------------------------------------------------------------

## Step 11: Create Jenkins Job

Dashboard → New Item → Freestyle Project\
Name: Local_Project

------------------------------------------------------------------------

## Step 12: Connect Local Repo

file:///home/YOUR_USERNAME/jenkins-local-project

------------------------------------------------------------------------

## Step 13: Enable Trigger

Poll SCM:

    * * * * *

------------------------------------------------------------------------

## Step 14: Add Build Step

``` bash
echo "Build Started"
python3 app.py
echo "Build Finished"
```

------------------------------------------------------------------------

## Step 15: Save and Build

Click Save → Build Now → Check Console Output

------------------------------------------------------------------------

## Step 16: Trigger from Terminal

``` bash
nano app.py
```

Change:

``` python
print("Build Triggered from Terminal")
```

Then:

``` bash
git add .
git commit -m "Updated code"
```

Wait 1 minute

------------------------------------------------------------------------

## Step 17: Verify

Jenkins → Build History → Console Output

Expected: Build Started\
Build Triggered from Terminal\
Build Finished

------------------------------------------------------------------------

## Output

Jenkins automatically triggers builds using local Git changes.

------------------------------------------------------------------------

## Viva Points

-   Jenkins automates builds\
-   Git tracks changes\
-   Poll SCM triggers builds\
-   Offline method

------------------------------------------------------------------------

## Memory Commands

``` bash
git init
git add .
git commit -m "msg"
```
