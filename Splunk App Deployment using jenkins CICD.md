
**Step 1: Creating a GitHub repository for the source code of Splunk App**

This documentation provides step-by-step instructions for deploying the Splunk app from Splunkbase to a local system and subsequently pushing it to a GitHub repository using GitBash.

**Prerequisites**
Before starting the deployment process, ensure that the following prerequisites are met:
Splunk Account: Create an account on Splunkbase (https://splunkbase.splunk.com/app/1928) if you do not have one.
GitBash: Install GitBash on your local system. You can download it from https://gitforwindows.org/.
GitHub Account: Create a GitHub account (https://github.com/) if you do not have one.

**Deployment Steps**
1. Download and Unzip Splunk App.
Click on login to download..
Navigate to the Splunk app download page: Download.
Download the app file and unzip it on your local system.
2. Configure GitBash
Navigate to the directory where you have downloaded and unzipped the Splunk app using the cd command.
Open GitBash on your local system.
Set your Git username and email using the following commands:
```
git config user.name "YourName"
git config user.email "yourname@gmail.com"
```
3. Initialize Git Repository
Initialize a Git repository in this directory:	
```	
git init
```
4. Add and Commit Files
```
git add appname
```
5. Commit the changes with a meaningful message:
```
git commit -m "Initial commit"
```
6. Connect to GitHub Repository
Create a new repository on GitHub.
Use the following commands to add the GitHub repository as the remote origin:
```
git remote add origin "YourGitHubRepositoryURL"
```
8. Push to GitHub
Push the committed changes to the master branch of the GitHub repository:
```
git push -u origin master
```
10. Verify on GitHub
Visit your GitHub repository to verify that the app folder has been successfully pushed.


**Step 2: Spinning up EC2 instance and installing all the packages (Java)**
Sign in to AWS Console:
Go to the AWS Management Console (https://aws.amazon.com/console/) and sign in.
Navigate to EC2:
In the AWS Management Console, navigate to the EC2 service by clicking on "Services" in the top menu and selecting "EC2" under the "Compute" section.
Launch an Instance:
Click on the "Launch Instance" button to start the EC2 instance creation process.
Choose an Amazon Machine Image (AMI):
Select an AMI for your instance. You can choose from a variety of Linux and Windows AMIs. For example, you can choose an Amazon Linux 2 AMI.
Choose an Instance Type:
Select an instance type based on your requirements. The instance type determines the hardware capabilities of your EC2 instance.
Configure Instance Details:
Configure instance details such as the number of instances, network settings, and IAM role. You can use the default settings for most options.
Add Storage:
Configure the storage settings for your instance. You can add additional EBS volumes if needed.
Configure Security Group:
Configure the security group to control inbound and outbound traffic to your instance. You'll need to open ports for SSH (22) and any other services you plan to run.(Note :customTCP: port(8000); All traffic(22))
Review and Launch:
Review your instance configuration and click on "Launch" to launch your EC2 instance.
Install Packages:
Once connected to your instance, you can install packages using the package manager for your distribution. For example, on Amazon Linux 2, you can use yum/apt depend on OS
```		
sudo yum/apt update -y
sudo yum/apt install package-name
sudo apt update
sudo apt install openjdk-17-jre
```


**Step 3: Installing the Jenkins and installing the required plugins for deployments**
```
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins
```

Note: Access the jenkins portal using IPAddress:8080 
For first login to Jenkins : 
```
cat /var/lib/jenkins/secrets/initialAdminPassword 
```



**Step 4: Creating a Freestyle project to get the source code from GitHub to deploy into the Splunk**
Create a New Jenkins Freestyle Project:
Click on "New Item" on the Jenkins dashboard.
Enter a name for your project (e.g., "Deploy to Splunk").
Select "Freestyle project" and click "OK" to create the project.
Configure Source Code Management (SCM):
In the project configuration, under "Source Code Management," select "Git".
Enter the repository URL of your GitHub repository.
Select the credentials you created earlier.
Configure any additional settings as needed for your repository.

Configure Build Steps:
In the project configuration, under "Build," click on "Add build step" and select "Execute shell" (for Linux/macOS) or "Execute Windows batch command" (for Windows).
Enter the shell commands or batch commands to deploy the source code into Splunk. For example

Save and Run the Jenkins Job:
Save your Jenkins project configuration.
Click on "Build Now" to run the Jenkins job and deploy the source code into Splunk.
Monitor the Build:
You can monitor the build progress and view the console output to see the deployment steps.

Note: After deploying(/opt/splunk/etc/apps) through jenkins we can see the output of app Splunk Add-on ServiceNow in splunk enterprise
