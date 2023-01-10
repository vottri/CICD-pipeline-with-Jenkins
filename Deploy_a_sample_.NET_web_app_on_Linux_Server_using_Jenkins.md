

Update your system
```sh
sudo apt-get update
```


## Installing Git

Git is likely already installed in your Ubuntu 20.04 server. You can confirm this is the case on your server with the following command:

```sh
git --version
```

![git1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/git1.png)

However, if you did not get output of a Git version number, you can install Git with:

```sh
sudo apt-get install git
```

## Installing .NET

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
sudo apt-get update 
```

.NET is made up of the runtime and the SDK. The .NET SDK allows you to create .NET apps and libraries. The runtime allows you to run apps that were made with .NET.

Install the SDK (which includes the runtime) if you want to develop .NET apps. If you only need to run apps, install the Runtime; more specifically, install the ASP.NET Core Runtime as it includes both .NET and ASP.NET Core runtimes.

**Install .NET SDK 6.0**

```sh
sudo apt-get -y install dotnet-sdk-6.0
```

**Install ASP.NET Core Runtime 3.1**

The ASP.NET Core Runtime allows you to run apps that were made with .NET 

Note: You should check which .NET core version you are using in your application and install the one you want: 

```sh
sudo apt-get -y install aspnetcore-runtime-3.1	
```

dotnet --version

dotnet --list-sdks and dotnet --list-runtimes

## Installing Java

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

## Installing Jenkins

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

•	Setup Jenkins as a daemon launched on start. Run systemctl cat jenkins for more details.
•	Create a ‘jenkins’ user to run this service.
•	Direct console log output to systemd-journald. Run journalctl -u jenkins.service if you are troubleshooting Jenkins.
•	Populate /lib/systemd/system/jenkins.service with configuration parameters for the launch, e.g JENKINS_HOME
•	Set Jenkins to listen on port 8080. Access this port with your browser to start configuration.

Start Jenkins:

```sh
sudo systemctl start jenkins
```

![jenkins1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins1.png)

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

Keep your Jenkins URL. Click Save and Finish.

![jenkins4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins4.png)

When the Jenkins is ready page appears, click Start using Jenkins.

![jenkins5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins5.png)

Jenkins Welcome Dashboard.

![jenkins6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins6.png)

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

![jenkins8](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/jenkins8.png)

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
Crate a directory where you deploy your web application

```sh
sudo mkdir -p /www/devopsweb
sudo chown -R root:jenkins /www/
sudo chmod -R 775 /www/
```

```sh
sudo visudo -f /etc/sudoers
```
![sudo](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/sudo.png)

```sh
sudo usermod -aG sudo jenkins
```
![sudo1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/sudo1.png)

```sh
sudo nano /etc/systemd/system/devopsweb.service
```
```sh
[Unit]
Description=Example .NET Web API App running on Ubuntu

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
```sh
sudo systemctl enable devopsweb.service
```
build


Installing Nginx

NGINX is open source software for web serving, reverse proxying, caching, load balancing,... In this lab we use NGINX as a web server.

Install Nginx

```sh
sudo apt-get -y install nginx
```

Start Nginx Server

```sh
sudo systemctl start nginx
```

![nginx](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/nginx.png)

```sh
sudo nano /etc/nginx/sites-available/devopsweb
```
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
```sh
sudo ln -s /etc/nginx/sites-available/devopsweb /etc/nginx/sites-enabled/devopsweb
```


sudo apt-get install snapd

sudo snap install core

sudo snap install --classic certbot

sudo ln -s /snap/bin/certbot /usr/bin/certbot

sudo certbot --nginx

sudo systemctl restart nginx
