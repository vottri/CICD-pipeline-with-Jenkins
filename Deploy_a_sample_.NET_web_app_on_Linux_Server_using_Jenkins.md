

Update your system
```sh
sudo apt-get update
```


Installing Git

Git is likely already installed in your Ubuntu 20.04 server. You can confirm this is the case on your server with the following command:

```sh
git --version
```

![git1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images2/git1.png)

However, if you did not get output of a Git version number, you can install Git with:

```sh
sudo apt-get install git
```

Installing .NET

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

.NET is made up of the runtime and the SDK. .NET SDK allows you to create .NET apps and libraries. The runtime allows you to run apps that were made with .NET.

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

Installing Jenkins

Installing Java

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


Install Jenkins

Before we can install Jenkins through the package manager, we’ll need to add the Jenkins Debian repository. Firstly, we’ll download the official PGP key from the Jenkins server and save it to /usr/share/keyrings/jenkins-keyring.asc:

You can choose between a LTS Release or Weekly Release

Long Term Support release

sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io.key
or
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee usr/share/keyrings/jenkins-keyring.asc 

Then, we add the Jenkins repository into the list:

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee  /etc/apt/sources.list.d/jenkins.list

Weekly release

sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io.key
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian binary/ | sudo tee  /etc/apt/sources.list.d/jenkins.list 

Finally update our local package index and install Jenkins:

sudo apt-get update
sudo apt-get -y install jenkins

The package installation will:

•	Setup Jenkins as a daemon launched on start. Run systemctl cat jenkins for more details.
•	Create a ‘jenkins’ user to run this service.
•	Direct console log output to systemd-journald. Run journalctl -u jenkins.service if you are troubleshooting Jenkins.
•	Populate /lib/systemd/system/jenkins.service with configuration parameters for the launch, e.g JENKINS_HOME
•	Set Jenkins to listen on port 8080. Access this port with your browser to start configuration.

Start Jenkins:
sudo systemctl start jenkins
sudo systemctl status jenkins


Unlock Jenkins

Browse to http://localhost:8080 and wait until the Unlock Jenkins page appears.

print the password at console.
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
On the Unlock Jenkins page, paste this password into the Administrator password field and click Continue.

Customize Jenkins with plugins

Choose Install suggested plugins to install the recommended set of plugins.

Create the first administrator user
..


click Save and Finish.

When the Jenkins is ready page appears, click Start using Jenkins.

Create a Personal Access Token in GitHub

In order for Jenkins to watch your GitHub projects, you will need to create a Personal Access Token in our GitHub account.

Visit GitHub and sign into your account. Click on your user icon in the upper-right hand corner and select Settings from the drop down menu.

On the page that follows, locate the Developer settings section on the left-hand menu and click Personal access tokens.

Click on Generate new token button on the next page
