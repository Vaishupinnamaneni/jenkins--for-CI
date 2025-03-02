AWS Jenkins Setup Documentation
Introduction
This document provides detailed steps to set up a Jenkins server on Amazon Web Services (AWS). Jenkins is an open-source automation server that enables developers to build, test, and deploy their software projects continuously.

Prerequisites
AWS account
Basic knowledge of AWS services
SSH key pair for connecting to EC2 instances
Steps to Set Up Jenkins Server on AWS
1. Launch an EC2 Instance
Sign in to AWS Management Console:

Navigate to the AWS Management Console.
Sign in with your credentials.
Navigate to EC2 Dashboard:

In the AWS Management Console, select "Services" and then choose "EC2" under the "Compute" section.
Launch an Instance:

Click on "Launch Instance."
Choose an Amazon Machine Image (AMI): Select the Amazon Linux 2 AMI or Ubuntu Server 20.04 LTS.
Choose an Instance Type: Select t2.micro (suitable for testing or small load).
Configure Instance Details: Use the default settings.
Add Storage: Configure as necessary (default is usually sufficient).
Add Tags: Optionally, add tags to your instance for easier identification.
Configure Security Group:
Create a new security group.
Add rules to allow HTTP (port 80), HTTPS (port 443), and SSH (port 22).
Review and Launch:

Click "Review and Launch."
Click "Launch" and select your existing key pair or create a new one.
Acknowledge that you have access to the selected key pair.
2. Connect to the EC2 Instance
Get the Public DNS/IP:

Go to the EC2 dashboard.
Select your running instance and note its public DNS or IP address.
Connect via SSH:

Open a terminal on your local machine.
Use the following command to connect (replace your-key.pem and ec2-user@your-ec2-public-ip):
bash
Copy Code


ssh -i "your-key.pem" ec2-user@your-ec2-public-ip
3. Install Java on the Instance
Jenkins requires Java to run.

Update the package index:

bash
Copy Code


sudo yum update -y   # For Amazon Linux
sudo apt-get update  # For Ubuntu
Install Java:

bash
Copy Code


sudo yum install java-1.8.0-openjdk-devel -y  # For Amazon Linux
sudo apt-get install openjdk-11-jdk -y         # For Ubuntu
Verify Java Installation:

bash
Copy Code


java -version
4. Install Jenkins
Add Jenkins repository:

bash
Copy Code


# For Amazon Linux
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key

# For Ubuntu
wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt-get update
Install Jenkins:

bash
Copy Code


sudo yum install jenkins -y  # For Amazon Linux
sudo apt-get install jenkins -y  # For Ubuntu
Start Jenkins service:

bash
Copy Code


sudo systemctl start jenkins
sudo systemctl enable jenkins
Check Jenkins status:

bash
Copy Code


sudo systemctl status jenkins
5. Configure Jenkins
Open Jenkins in a web browser:

Navigate to http://your-ec2-public-ip:8080.
Retrieve initial admin password:

bash
Copy Code


sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the password and paste it into the Jenkins setup wizard.
Complete the setup wizard:

Install suggested plugins.
Create your first admin user.
Configure Jenkins home directory if necessary:

This step is optional and depends on your needs.
Conclusion
By following these steps, you can successfully set up a Jenkins server on AWS. This setup will allow you to harness the power of Jenkins for continuous integration and continuous delivery (CI/CD) in your projects.

Commit and Push the Documentation
Commit the changes:

bash
Copy Code


git add awsjenkins-setup.md
git commit -m "Add Jenkins setup documentation for AWS"
Push the changes:

bash
Copy Code


git push origin feature-gcp-jenkins
This completes the documentation for setting up a Jenkins server on AWs
