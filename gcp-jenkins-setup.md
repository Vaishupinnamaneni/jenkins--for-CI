GCP Jenkins Setup Documentation
Introduction
This document provides detailed steps to set up a Jenkins server on Google Cloud Platform (GCP). Jenkins is an open-source automation server that helps automate parts of the software development process related to building, testing, and deploying.

Prerequisites
Google Cloud account
Basic knowledge of GCP services
SSH key pair for connecting to the VM instance
Steps to Set Up Jenkins Server on GCP
1. Create a Google Cloud Project
Log in to Google Cloud Console:

Navigate to the Google Cloud Console.
Sign in with your credentials.
Create a New Project:

In the top navigation bar, click on the project dropdown menu and select "New Project."
Enter a project name and organization (if applicable).
Click "Create."
2. Create a VM Instance
Navigate to the Compute Engine:

In the Google Cloud Console, go to the "Compute Engine" section.
Create an Instance:

Click on "Create Instance."
Configure instance details:
Name: Enter a name for your VM (e.g., jenkins-server).
Region and Zone: Select a region and zone near you.
Machine Type: Choose a machine type (e.g., n1-standard-1 for a small setup).
Boot disk: Click "Change" to select a boot disk. Choose Ubuntu 20.04 LTS or another preferred Linux distribution.
Firewall: Allow HTTP and HTTPS traffic.
Create the VM Instance:

Click "Create" to launch the VM instance.
3. Connect to the VM Instance
Get the External IP Address:

Navigate to the "VM instances" section in the Google Cloud Console.
Note the external IP address of your VM instance.
Connect via SSH:

From the Google Cloud Console, click on "SSH" next to your VM instance or use the following command in your terminal (replace your-vm-external-ip with your VM's IP address):
bash
Copy Code


gcloud compute ssh --zone "your-zone" "your-instance-name" --project "your-project-id"
4. Install Java on the VM Instance
Update the package index:

bash
Copy Code


sudo apt update
Install Java:

bash
Copy Code


sudo apt install openjdk-11-jdk -y
Verify Java Installation:

bash
Copy Code


java -version
5. Install Jenkins
Add Jenkins repository:

bash
Copy Code


wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo apt update
Install Jenkins:

bash
Copy Code


sudo apt install jenkins -y
Start Jenkins service:

bash
Copy Code


sudo systemctl start jenkins
sudo systemctl enable jenkins
Check Jenkins status:

bash
Copy Code


sudo systemctl status jenkins
6. Configure Jenkins
Open Jenkins in a web browser:

Navigate to http://your-vm-external-ip:8080.
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
By following these steps, you can successfully set up a Jenkins server on GCP. This setup will allow you to use Jenkins for continuous integration and continuous delivery (CI/CD) in your software projects.

Commit and Push the Documentation
Commit the changes:

bash
Copy Code


git add gcpjenkins-setup.md
git commit -m "Add Jenkins setup documentation for GCP"
Push the changes:

bash
Copy Code


git push origin feature-final-jenkins-review
This completes the documentation for setting up a Jenkins server on GCP.



