# Jenkins Build Trigger (Local Git + Webhook) - Ultra Beginner Guide

## AIM

Configure Jenkins to trigger builds using: 1. Local Git (offline safe)
2. GitHub Webhook (online method)

------------------------------------------------------------------------

# PART 1: LOCAL GIT METHOD (RECOMMENDED)

## Step 1: Install Jenkins

sudo apt update sudo apt install openjdk-11-jdk -y sudo apt install
jenkins -y

sudo systemctl start jenkins sudo systemctl enable jenkins

## Step 2: Open Jenkins

http://localhost:8080

Get password: sudo cat /var/lib/jenkins/secrets/initialAdminPassword

Install suggested plugins

------------------------------------------------------------------------

## Step 3: Install Git

sudo apt install git -y git --version

------------------------------------------------------------------------

## Step 4: Create Project Folder

mkdir jenkins-local-project cd jenkins-local-project

## Step 5: Create Python File

nano app.py

Paste: print("Hello from Jenkins")

------------------------------------------------------------------------

## Step 6: Initialize Git

git init git add . git commit -m "initial"

------------------------------------------------------------------------

## Step 7: Fix Permissions (IMPORTANT)

sudo chmod -R 777 \~/jenkins-local-project

------------------------------------------------------------------------

## Step 8: Create Jenkins Job

Dashboard → New Item → Freestyle Project

Name: Local_Project

------------------------------------------------------------------------

## Step 9: Connect Local Repo

file:///home/YOUR_USERNAME/jenkins-local-project

------------------------------------------------------------------------

## Step 10: Enable Trigger

Poll SCM: \* \* \* \* \*

------------------------------------------------------------------------

## Step 11: Build Step

Execute Shell:

echo "Build Start" python3 app.py echo "Build End"

------------------------------------------------------------------------

## Step 12: Trigger from Terminal

nano app.py (Change text)

git add . git commit -m "update"

WAIT 1 minute → Jenkins runs automatically

------------------------------------------------------------------------

# PART 2: GITHUB WEBHOOK METHOD

## Step 1: Create GitHub Repo

Go to GitHub → New Repo → jenkins-demo

## Step 2: Add File

Create add.py:

a=10 b=20 print(a+b)

------------------------------------------------------------------------

## Step 3: Clone Repo

git clone https://github.com/your-username/jenkins-demo.git cd
jenkins-demo

------------------------------------------------------------------------

## Step 4: Create Jenkins Job

Freestyle Project → Webhook_Project

------------------------------------------------------------------------

## Step 5: Connect Repo

https://github.com/your-username/jenkins-demo.git

Branch: \*/main

------------------------------------------------------------------------

## Step 6: Build Step

echo "Start" python3 add.py echo "End"

------------------------------------------------------------------------

## Step 7: Enable Webhook

Select: GitHub hook trigger for GITScm polling

------------------------------------------------------------------------

## Step 8: Get IP

ip addr

Example: 192.168.1.5

Webhook URL: http://192.168.1.5:8080/github-webhook/

------------------------------------------------------------------------

## Step 9: Add Webhook in GitHub

Repo → Settings → Webhooks

Payload: http://192.168.1.5:8080/github-webhook/

Content type: application/json

Event: Push

------------------------------------------------------------------------

## Step 10: Trigger Build

Edit file: git add . git commit -m "test" git push

------------------------------------------------------------------------

## OUTPUT

Jenkins triggers builds automatically using both methods.

------------------------------------------------------------------------

## VIVA POINTS

-   Local method uses Poll SCM
-   Webhook uses push events
-   Jenkins automates builds
-   Git tracks changes

------------------------------------------------------------------------

## MEMORY COMMANDS

git init git add . git commit -m "msg" git push
