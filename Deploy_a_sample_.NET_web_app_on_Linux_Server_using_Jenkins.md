# Deploy a sample .NET web app on Linux Server virtual machine using Jenkins

============================================================================================

**CONTENTS**

[1. Lab Setup](#1)

[2. Installing Git](#2)

[3. Installing .NET](#3)

[4. Installing Java ](#4)

[5. Installing Jenkins](#5)

[6. Configuring Jenkins](#6)

[7. Creating Jenkins Pipeline](#7)

[8. Hosting ASP.NET Core Web App using Nginx](#8)

[9. Configuring SSL Certficate](#9)

============================================================================================

## 1. Lab Setup <a name="1"></a>

### Create a Linux Server Virtual Machine on Azure (OS: Ubuntu 20.04)

![ub01-1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/ub01-1.png)

### Connect to your Virtual Machine

Navigate to "Networking" tab > "Inbound port rules" section, allow your VM's ports 80, 443, 22 to be accessible from the Internet.

![ub01-2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/ub01-2.png)

Use **PuTTY** for connecting to the Linux Virtual Machine. Enter your Linux machine's public IP address in Host Name and Port will be 22. Click on **Open** button to connect.

![ub01-3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/ub01-3.png)

When you are inside the Linux VM:

![ub01-4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/ub01-4.png)

Check for working Internet connection.

Update your system

```sh
sudo apt-get update
```

Install some required packages:

```sh
sudo apt-get -y install wget apt-transport-https
```

## 2. Installing Git <a name="2"></a>

Git is likely already installed in your Ubuntu 20.04 server. You can confirm this is the case on your server with the following command:

```sh
git --version
```

![git1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/git1.png)

However, if you did not get output of a Git version number, you can install Git with:

```sh
sudo apt-get install git
```

## 3. Installing .NET <a name="3"></a>

**Check whether .NET is already installed**

```sh
dotnet --version
```

**Register Microsoft key and feed**

Before installing .NET, you’ll need to register the Microsoft key, register the product repository, and install required dependencies. 

```sh
wget https://packages.microsoft.com/config/ubuntu/20.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
```

.NET is made up of the runtime and the SDK. The .NET SDK allows you to create .NET apps and libraries. The runtime allows you to run apps that were made with .NET.

Install the SDK (which includes the runtime) if you want to develop .NET apps. If you only need to run apps, install the Runtime; more specifically, install the ASP.NET Core Runtime as it includes both .NET and ASP.NET Core runtimes.

**Install .NET SDK 6.0**

```sh
sudo apt-get update 
sudo apt-get -y install dotnet-sdk-6.0
```

**Install ASP.NET Core Runtime 3.1**

The ASP.NET Core Runtime allows you to run apps that were made with .NET 

Note: You should check which .NET core version you are using in your application and install the one you want: 

```sh
sudo apt-get -y install aspnetcore-runtime-3.1	
```

![dotnet](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/dotnet.png)

## 4. Installing Java <a name="4"></a>

Jenkins requires Java in order to run, yet certain distributions don’t include this by default and some Java versions are incompatible with Jenkins.

**Check whether Java is already installed**

```sh
java --version
```

**Install Java**

```sh
sudo apt-get update
sudo apt-get -y install openjdk-11-jre
```

![java1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/java1.png)

## 5. Installing Jenkins <a name="5"></a>

Before we can install Jenkins through the package manager, we’ll need to add the Jenkins Debian repository. Firstly, we’ll download the official PGP key from the Jenkins server and save it to /usr/share/keyrings/jenkins-keyring.asc:

```sh
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io.key
```

Then, we add the Jenkins repository into the list:

```sh
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee  /etc/apt/sources.list.d/jenkins.list
```

Finally update our local package index and install Jenkins:

```sh
sudo apt-get update
sudo apt-get -y install jenkins
```

The package installation will:

 - Setup Jenkins as a daemon launched on start. Run systemctl cat jenkins for more details.
 - Create a ‘jenkins’ user to run this service.
 - Direct console log output to systemd-journald. Run journalctl -u jenkins.service if you are troubleshooting Jenkins.
 - Populate /lib/systemd/system/jenkins.service with configuration parameters for the launch, e.g JENKINS_HOME
 - Set Jenkins to listen on port 8080. Access this port with your browser to start configuration.

Start Jenkins:

```sh
sudo systemctl start jenkins
```

Check the status of the Jenkins service

![jenkins1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins1.png)

## 6. Configuring Jenkins <a name="6"></a>

### Post-installation setup wizard

Unlock Jenkins

Open a web broswer, type [http://Jenkins server public IP:8080] and wait until the Unlock Jenkins page appears.

![jenkins2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins2.png)

Go to Jenkins server, print the password at console.

```sh
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

On the Unlock Jenkins page, paste this password into the Administrator password field and click Continue.

On the next page, choose "Install suggested plugins" to install the recommended set of plugins.

![jenkins3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins3.png)

Create the first administrator user

![jenkins11](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins11.png)

Keep your Jenkins URL. Click "Save and Finish".

![jenkins4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins4.png)

When the Jenkins is ready page appears, click "Start using Jenkins".

![jenkins5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins5.png)

Jenkins Welcome Dashboard.

![jenkins6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins6.png)

### Connect Jenkins to Github

**Create a Personal Access Token in GitHub**

In order for Jenkins to watch your GitHub projects, you will need to create a Personal Access Token in our GitHub account.

Visit GitHub and sign into your account. Click on your user icon in the upper-right hand corner and select Settings from the drop down menu.

On the page that follows, locate the Developer settings section on the left-hand menu and click Personal access tokens.

![gh1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh1.png)

Click on Generate new token button on the next page. Also choose Generate new token (classic).

![gh2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh2.png)

Give your token a name refer to your intergration with Jenkins. In the Select Scopes section, choose the same as below:

![gh3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh3.png)
 
When you are finished, click Generate token at the bottom.

You get a token.

![gh4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh4.png)
 
Copy the token now so that we can reference it later. As the message indicates, there is no way to retrieve the token once you leave this page.

Note: 
As mentioned in the screenshot above, for security reasons, there is no way to redisplay the token once you leave this page. If you lose your token, delete the current token from your GitHub account and then create a new one.

**Add the GitHub Personal Access Token to Jenkins**

Now that you have a personal access token for your GitHub account, we can configure Jenkins to watch your project’s repository.

Log into your Jenkins web interface using the administrative account you configured during installation.

Click on your username in the top-right corner to access your user settings, and from there, click Credentials in the left-hand menu.

![jenkins8-1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins8-1.png)

On the next page, click the arrow next to (global) across System (Stores from parent). In the box that appears, click Add credentials:

![gh6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh6.png)

Fill out all the fields same as below:

![gh7](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh7.png)

Click the "Create" button when you are finished.

![jenkins7](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins7.png)

Once you are done, restart Jenkins once.

```sh
sudo systemctl restart jenkins
```

## 7. Creating Jenkins Pipeline <a name="7"></a>

### Create a directory where you deploy your web application

```sh
sudo mkdir -p /www/devopsweb
sudo chown -R root:jenkins /www/
sudo chmod -R 775 /www/
```

### Create a systemd file for your web application (run your webapp as a service).

```sh
sudo nano /etc/systemd/system/devopsweb.service
```

Fill in the file with these configurations

```sh
[Unit]
Description=Example .NET Web App running on Ubuntu 

[Service]
WorkingDirectory=/www/devopsweb/
ExecStart=/www/devopsweb/DevOpsWeb
Restart=always
RestartSec=10
KillSignal=SIGINT
User=jenkins
Environment=ASPNETCORE_ENVIRONMENT=Production

[Install]
WantedBy=multi-user.target
```

Enable the created webapp service 

```sh
sudo systemctl enable devopsweb.service
```

### Enable Running shell scripts in jenkins

Jenkins talks to your linux server with a user called “jenkins”. But running shell commands which have "sudo" might not worked as the "jenkins" user doesn’t have access to read passwords from your linux server. We might want to tell the Linux Server not to ask password while executing commands for the "jenkins" user.

Edit the /etc/sudoers file to provide permission to Jenkins user.

```sh
sudo visudo -f /etc/sudoers
```
![sudo](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/sudo.png)

Add the Jenkins user to sudo group.
```sh
sudo usermod -aG sudo jenkins
```

![sudo1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/sudo1.png)

### Create a pipeline to build your application

On the Jenkins dashboard, click on "New Item". 

![jenkins8-3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins8-3.png)

Enter an item name, for example, "devopsweb" and select the "Pipeline" project. Then click OK.

![jenkins8-2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins8-2.png)

In the Configuration Dashboard, click the "Pipeline" button on the left menu:

Scroll down to the "Script" section, and insert the steps needed for running a Jenkins Pipeline then save the changes.

![jenkins9](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins9.png)

Components of Jenkins Pipeline:

 - The pipeline consists of all the instructions to build, test, and deliver software. It is the key component of a Jenkins Pipeline.

 - An agent is assigned to execute the pipeline on a node and allocate a workspace for the pipeline.

 - A stage is a block that has steps to build, test, and deploy the application. Stages are used to visualize the Jenkins Pipeline processes.

 - A step is a single task to be performed, for example, create a directory, run a docker image, delete a file, etc.

```sh
pipeline {
    agent any 
    
    stages {
        stage('Clone') {
            steps {
                git branch: 'master',
                    credentialsId: 'github_key',
                    url: ‘https://github.com/vottri/DevOpsRepo.git'
            }
        }
        
        stage('Build') {
            steps {
                sh '''
                    sudo systemctl stop devopsweb.service
                    dotnet publish DevOpsWeb/DevOpsWeb.csproj -c release -o /www/devopsweb/
                    sudo systemctl start devopsweb.service
                '''
            }
        }
    }
    
    post {
        always {
            cleanWs()
        }
    }
}
```

--------------------------------------------------------------------------------------------
Note:

**agent** any      // *Any available agent is getting assigned to the pipeline*

**stage**('Clone') // *Retrieve code from a GitHub repository*

**stage**('Build') // *Compile the application, read through its dependencies specified in the project file, publish the resulting set of files to a folder* 

**steps**
```sh
systemctl stop / start       // Stop / Start the web app service
dotnet publish               // Publish the application and its dependencies to a folder for deployment to a hosting system
```
-------------------------------------------------------------------------------------------

After saving your configures:

On the left-side navigation pane, click "Build Now" to start the pipeline. After Jenkins pipeline is done running, the output should look like this.

![jenkins10](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins10.png)

You can hover the cursor over the stages in "Stage View" section and choose "View Logs" to see detailed logs of every stages.

Logs from "Clone" Stage:

![log1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/log1.png)

Logs from "Build" Stage:

![log2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/log2.png)

Logs from Post Actions: clean workspace

![log3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/log3.png)

Your web app directory after the build.

![webapp2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/webapp2.png)

Check your web app service.

![webapp-1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/webapp-1.png)

## 8. Hosting ASP.NET Core Web App using Nginx <a name="8"></a>

NGINX is an open source software for web serving, reverse proxying, caching, load balancing,... In this lab we use NGINX as a web server.

### Install Nginx

```sh
sudo apt-get -y install nginx
```

Start Nginx Server

```sh
sudo systemctl start nginx
```

![nginx](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/nginx.png)

### Configure Nginx as a reverse proxy server

Configure Nginx as a reverse proxy to forward requests to ASP.NET Core app:

Create a new file /etc/nginx/sites-available/devopsweb for your webapp. 
```sh
sudo nano /etc/nginx/sites-available/devopsweb
```
Fill in the contents as the following:
```sh
server {
    listen 80;
    server_name 127.0.0.1;
    location / {
        proxy_pass         https://127.0.0.1:5001;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

Create a symlink for your webapp in the sites-enabled directory:

```sh
sudo ln -s /etc/nginx/sites-available/devopsweb /etc/nginx/sites-enabled/devopsweb
```

Remove the default website in the sites-enabled directory:

```sh
sudo rm /etc/nginx/sites-enabled/default
```

Restart nginx server.

```sh
sudo systemctl restart nginx
```
### Access your website over the Internet

After verifying nginx is working, let’s check your web application is running or not by typing the server's public IP address in the browser.

![web1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/web1.png)

Register a Domain Name for your website and make sure it DNS record point to your public IP address.

![matbao](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/matbao.jpg)

Modify your nginx web site configuration file

```sh
sudo nano /etc/nginx/sites-available/devopsweb
```

Replace the server name with your registered domain name.

```sh
server {
    listen 80;
    server_name mnandnt.com;
    location / {
        proxy_pass         https://127.0.0.1:5001;
        proxy_http_version 1.1;
        proxy_set_header   Upgrade $http_upgrade;
        proxy_set_header   Connection keep-alive;
        proxy_set_header   Host $host;
        proxy_cache_bypass $http_upgrade;
        proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header   X-Forwarded-Proto $scheme;
    }
}
```

Restart nginx server.

```sh
sudo systemctl restart nginx
```

Acess your web site with the new domain name.

![web2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/web2.png)

## 9. Configuring SSL Certificate <a name="9"></a>

Switch your website from HTTP to HTTPS using Certbot.

Certbot is a free, open source software tool for automatically using Let’s Encrypt certificates on websites to enable HTTPS for them. 

Install snapd

```sh
sudo apt-get install snapd
```

Ensure that you have the latest version of snapd.

```sh
sudo snap install core
sudo snap refresh core
```

![cert-0](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/cert-0.png)

Install Certbot

```sh
sudo snap install --classic certbot
```

![cert-1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/cert-1.png)

Ensure that the certbot command can be run.

```sh
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

Run this command to get a certificate and have Certbot edit your nginx configuration automatically to serve it, turning on HTTPS access in a single step.

```sh
sudo certbot --nginx
```

![cert2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/cert2.png)

Continue to answer the question with the appropriate site name and let Certbot handle it.

![cert3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/cert3.png)

You might want to restart your nginx server.

```sh
sudo systemctl restart nginx
```

Your site after completing Certbot process.

![cert4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/cert4.png)

To confirm that your site is set up securely, visit your website with HTTPS.

![https1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/https1.png)

Check SSL Certificate.

![https2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/https2.png)

