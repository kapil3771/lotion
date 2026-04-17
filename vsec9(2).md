# Jenkins Build Trigger using GitHub Webhook (Ultra Noob Version)

## Aim

To configure Jenkins so that it automatically runs a Python program
whenever code is pushed to GitHub.

------------------------------------------------------------------------

## Requirements

-   Ubuntu system\
-   Internet connection\
-   GitHub account\
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

## Step 3: Start Jenkins

``` bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
```

------------------------------------------------------------------------

## Step 4: Open Jenkins

Open browser: http://localhost:8080

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

## Step 7: Create GitHub Repository

1.  Open https://github.com\
2.  Click **New Repository**\
3.  Name: jenkins-demo\
4.  Do NOT initialize with README\
5.  Click Create Repository

------------------------------------------------------------------------

## Step 8: Add Python File (GitHub UI)

1.  Click **Add file → Create new file**\
2.  File name: add.py

Paste:

``` python
a = 10
b = 20
print("Addition is:", a+b)
```

3.  Click **Commit changes**

------------------------------------------------------------------------

## Step 9: Clone Repository Locally

``` bash
cd ~
git clone https://github.com/your-username/jenkins-demo.git
cd jenkins-demo
```

------------------------------------------------------------------------

## Step 10: Create Jenkins Job

Dashboard → New Item\
Name: Webhook_Project\
Select: Freestyle Project

------------------------------------------------------------------------

## Step 11: Connect GitHub Repo

Go to: Configure → Source Code Management → Git

Paste: https://github.com/your-username/jenkins-demo.git

Branch: \*/main

------------------------------------------------------------------------

## Step 12: Add Build Step

Go to Build → Execute Shell

``` bash
echo "Build Started"
python3 add.py
echo "Build Finished"
```

------------------------------------------------------------------------

## Step 13: Enable Webhook Trigger

Go to Build Triggers

Enable: GitHub hook trigger for GITScm polling

------------------------------------------------------------------------

## Step 14: Get System IP

``` bash
ip addr
```

Look for: 192.168.x.x

------------------------------------------------------------------------

## Step 15: Configure GitHub Webhook

Go to: Repository → Settings → Webhooks → Add Webhook

Fill:

Payload URL: http://YOUR_IP:8080/github-webhook/

Content type: application/json

Event: Just the push event

Click Add Webhook

------------------------------------------------------------------------

## Step 16: Trigger Build

Edit file:

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

## Step 17: Verify

Go to: Jenkins → Webhook_Project → Build History → Console Output

Expected: Build Started\
Addition is: 30\
Webhook Triggered Successfully\
Build Finished

------------------------------------------------------------------------

## Output

Jenkins automatically triggers builds whenever code is pushed to GitHub.

------------------------------------------------------------------------

## Viva Points

-   Jenkins automates builds\
-   GitHub webhook triggers instantly\
-   No manual build required\
-   CI/CD concept

------------------------------------------------------------------------

## Memory Commands

``` bash
git clone <repo>
git add .
git commit -m "msg"
git push origin main
```
