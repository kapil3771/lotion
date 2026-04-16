# Jenkins Automated Build using GitHub Webhook (Beginner Friendly)

## Aim

To configure Jenkins so that it automatically runs a Python program
whenever code is pushed to GitHub.

------------------------------------------------------------------------

## Requirements

-   Ubuntu system
-   Internet connection
-   GitHub account
-   Basic terminal usage

------------------------------------------------------------------------

## Step 1: Install Jenkins (Ubuntu)

``` bash
sudo apt update
sudo apt install openjdk-11-jdk -y
sudo apt install jenkins -y
```

Start Jenkins:

``` bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

Check status:

``` bash
sudo systemctl status jenkins
```

------------------------------------------------------------------------

## Step 2: Open Jenkins in Browser

Open:

    http://localhost:8080

Get password:

``` bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

Paste it → Continue → Install suggested plugins

------------------------------------------------------------------------

## Step 3: Install Required Plugins

Go to:

    Manage Jenkins → Manage Plugins → Available

Install: - Git Plugin - GitHub Plugin

Restart Jenkins.

------------------------------------------------------------------------

## Step 4: Install Git (if not installed)

``` bash
sudo apt install git -y
git --version
```

------------------------------------------------------------------------

## Step 5: Create GitHub Repository (VERY BASIC)

1.  Open GitHub
2.  Click **New Repository**
3.  Name: `jenkins-demo`
4.  Click **Create Repository**

------------------------------------------------------------------------

## Step 6: Add Python File (add.py)

Option 1 (via GitHub UI): 1. Click **Add file → Create new file** 2.
File name: `add.py`

Paste:

``` python
a = 10
b = 20
print("Addition is:", a+b)
```

3.  Click **Commit changes**

------------------------------------------------------------------------

## Step 7: Clone Repository to Local

``` bash
git clone https://github.com/your-username/jenkins-demo.git
cd jenkins-demo
```

------------------------------------------------------------------------

## Step 8: Create Jenkins Job

1.  Open Jenkins Dashboard
2.  Click **New Item**
3.  Name: `Addition_Project`
4.  Select **Freestyle Project**
5.  Click OK

------------------------------------------------------------------------

## Step 9: Connect GitHub Repo

Go to **Configure → Source Code Management → Git**

Paste repo URL:

    https://github.com/your-username/jenkins-demo.git

Branch:

    */main

------------------------------------------------------------------------

## Step 10: Add Build Step

Scroll to **Build → Execute Shell**

``` bash
echo "Build Started"
python3 add.py
echo "Build Finished"
```

------------------------------------------------------------------------

## Step 11: Enable Webhook Trigger

In **Build Triggers**, check:

    GitHub hook trigger for GITScm polling

------------------------------------------------------------------------

## Step 12: Get System IP

``` bash
ip addr
```

Example:

    192.168.1.5

------------------------------------------------------------------------

## Step 13: Configure GitHub Webhook

Go to GitHub:

    Repo → Settings → Webhooks → Add Webhook

Fill:

Payload URL:

    http://192.168.1.5:8080/github-webhook/

Content type:

    application/json

Event:

    Just the push event

Click **Add Webhook**

------------------------------------------------------------------------

## Step 14: Trigger Build

Edit file locally:

``` bash
nano add.py
```

Change:

``` python
print("Webhook Triggered Successfully")
```

Then:

``` bash
git add .
git commit -m "Webhook test"
git push origin main
```

------------------------------------------------------------------------

## Step 15: Verify in Jenkins

Go to:

    Jenkins → Addition_Project → Build History → Console Output

Expected:

    Build Started
    Addition is: 30
    Webhook Triggered Successfully
    Build Finished
    Finished: SUCCESS

------------------------------------------------------------------------

## Output

Jenkins automatically runs the Python script whenever code is pushed to
GitHub using webhook.

------------------------------------------------------------------------

## Viva Points

-   Jenkins automates build process
-   GitHub webhook triggers Jenkins
-   CI/CD concept
-   No manual build required

------------------------------------------------------------------------

## Memory Commands

``` bash
git clone <repo>
git add .
git commit -m "msg"
git push origin main
```
