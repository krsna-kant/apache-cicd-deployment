# Jenkins and Apache Deployment Project

This project automates the deployment process of an Apache web server using Jenkins on an Ubuntu EC2 instance. It includes setting up Jenkins, Apache2, configuring the EC2 server, integrating Git for version control, making changes in the visudo file for permissions, and creating a webhook for GitHub repository updates.

## Prerequisites

Before starting, ensure you have:

- An Ubuntu EC2 instance set up with Apache2 installed.
- Jenkins installed and running on the EC2 instance.
- Git installed on the server for version control.
- Access to modify the visudo file for necessary permissions.
- A GitHub repository with your web application code.

## Setting up Jenkins Pipeline

1. Create a new Jenkins pipeline job.
2. Copy and paste the provided Jenkins pipeline script into your pipeline job configuration.
3. Replace the GitHub repository URL in the script (`https://github.com/krsna-kant/mark_ecommerce.git`) with your actual repository URL.
4. Save the pipeline job configuration.

## Adding Jenkins to visudo File

To grant Jenkins necessary permissions to execute commands as root (for example, restarting Apache), follow these steps:

1. Open the visudo file using the command `sudo visudo`.
2. Scroll down to the section where user privileges are defined.
3. Add the following line to grant Jenkins passwordless sudo access:
`jenkins ALL=(ALL) NOPASSWD: ALL`
Replace `jenkins` with the actual username of your Jenkins installation if it's different.
4. Save and exit the visudo file by pressing `Ctrl + X`, then `Y`, and finally `Enter`.

## Pipeline Overview

### Stage 1: Clone Code
- This stage clones the code from your GitHub repository using Git.

### Stage 2: Deploying Files To Apache
- Removes existing files in `/var/www/html/` directory.
- Moves the cloned files from the repository to the Apache web server directory.

### Stage 3: Restart Apache
- Restarts the Apache web server to apply changes made during deployment.

## Usage

1. Trigger the Jenkins pipeline manually or configure it to trigger automatically on code changes.
2. Jenkins will clone the code, deploy it to Apache, and restart the server.
3. Monitor the Jenkins job console output for deployment status and any errors.

## Notes

- Ensure proper permissions are set for Jenkins to execute commands such as restarting Apache (`sudo systemctl restart apache2`).
- Configure webhooks in your GitHub repository settings to trigger Jenkins builds automatically on code pushes.

