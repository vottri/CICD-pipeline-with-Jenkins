
============================================================================================

Contents

[1. Lab Setup](#1)

[2. Download](#2)

[3. Installing IIS and ASP.NET Modules](#3)

[4. Installing .NET SDK ](#4)

[5. Installing Git](#5)

[6. Installing Java SDK](#6)

[7. Installing Jenkins](#7)

[8. Configuring Jenkins](#8)

[9. Creating Jenkins Pipeline ](#9)

[10. domain and ssl](#10)

============================================================================================

## 1. Lab Setup <a name="1"></a>

## 2. Download <a name="2"></a>

Download .NET SDK 6.0 (https://dotnet.microsoft.com/en-us/download/dotnet/6.0).

![dotnet1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/dotnet1.png)

Download ASP.NET Core Runtime 3.1 (https://dotnet.microsoft.com/en-us/download/dotnet/3.1).

![dotnet2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/dotnet2.png)

Download Jenkins for Windows (https://www.jenkins.io/download/).

![jenkins](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins.png)

Download Java SE Development Kit 11.0.17 for Windows (https://www.oracle.com/java/technologies/downloads/#java11).

![java11](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/java11.png)

Download Git 2.39.0 for Windows (https://git-scm.com/download/win).

![git](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git.png)

Download ACME Client for Windows.

![acme](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/acme.png)

Downloaded Files.

![downloads](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/downloads.png)

## 3. Installing IIS and ASP.NET Modules <a name="3"></a>

### Installing IIS Server

On Windows Server, go to Server Manager. Click on the "Add roles and features" on the dashboard. Click ***Next*** to proceed.

Select "Role-based or feature-based installation", and then click ***Next***.

Select the server.

![iis1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis1.png)

Choose the "Web Server" option.

![iis2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis2.png)

Choose as below.

![iis3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis3.png)

Continue to proceed with below options.

![iis4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis4.png)

In the final screen, click the "Install" button to begin the installation. Once IIS has been installed, click "Close".

### Configuring IIS Server

Open Windows Explorer. Create a new directory for your web site.

![web1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web1.png)

In "Server Manager" Dashboard. Go to "Tools". Open "Internet Information Services Manager".

In IIS, you will have an initial site set up called "Default Web Site". We are not gonna use it.

Right-click "Default Web Site". Click "Edit Bindings". 

![web2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web2.png)

When "Site Bindings" dialogue box appears, click "Edit". Change Port to 8088. Click OK.

![web3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web3.png)

Create a new website.  

Right-click "Sites". Choose "Add Website".

![web4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web4.png)

Fill in the required information as below. Then Click OK.

![web5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web5.png)

![web6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web6.png)

## 4. Installing .NET SDK <a name="4"></a>

### Install .NET SDK 6.0

Double-click the installation package, and then click "Install" on the installation wizard.

![dotnet6](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet6.png)

Click "Close" once it has been installed successfully.

![dotnet3](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet3.png)

### Install ASP.NET Core Runtime 3.1 

Double-click the installation package, tick "I agree to license terms and conditions" then click "Install".

![dotnet4](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet4.png)

Click "Close" once it has been installed successfully.

![dotnet5](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet5.png)

## 5. Installing Git <a name="5"></a>

Go to your Downloads folder. Double click on downloaded Git application. Click ***Next*** to start installation of Git.

![git1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git1.png)

***Next***.

![git2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git2.png)

***Next***.

![git3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git3.png)

***Next***.

![git4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git4.png)

***Next***.

![git5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git5.png)

Select “Checkout as-is,Commit Unix-Style line endings” and Click ***Next***.

![git6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git6.png)

***Next***.

![git7](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git7.png)

***Next***.

![git8](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git8.png)

***Next***.

![git9](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git9.png)

Tick "Enable symbolic links" and click ***Next***.

![git10](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git10.png)

Click ***Install***.

![git12](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git12.png)

Click ***Finish***.

![git11](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/git11.png)

## 6. Installing Java SDK <a name="6"></a>

### Install Java Development Kit

Go to where you have downloaded the JDK application on your machine and double click the application. Click ***Next*** to start the installation.

![jv1](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv1.png)

***Next***.

![jv2](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv2.png)

Wait till the installation is completed and click ***Close***.

![jv3](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv3.png)

### Set the Path for the Environmental Variable for JDK

Open the Windows Run prompt, type ***sysdm.cpl*** and hit Enter.

In the new window that opens, click on the "Advanced" tab and then click on the "Environment Variables" button.

![jv4](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv4.png)


![jv5](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv5.png)

Click on "New" in both "User variables" and "System variables" box to create a new variable:

 - Give Variable name: “JAVA_HOME”

 - Give Variable value: the path of Java installation folder "C:\Program Files\Java\jdk-11.0.17"

![jv6](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv6.png)

In the "System variables" box, select "Path" and click on "Edit". Another dialogue box opens, click on "New":

Type “C:\Program Files\Java\jdk-11.0.17\bin” 

Click on "New" again: 

Type "%SystemRoot%\System32\inetsrv"

When you 're done, Click OK.

![jv7](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv7.png)


![jv8](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv8.png)

## 7. Installing Jenkins <a name="7"></a>

Double click on the Jenkins installation file to start the installation. You should see the Jenkins welcome page. Click ***Next***.

![jenkins1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins1.png)

***Next***.

![jenkins2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins2.png)

***Next***.

![jenkins3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins3.png)

Define your Jenkins port and click on the "Test Port" button to test the port. If the port is available, you should see the following result. Click ***Next*** to continue.

![jenkins4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins4.png)

***Next***.

![jenkins5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins5.png)

***Next***.

![jenkins6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins6.png)

Click ***Install***. 

![jenkins7](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins7.png)

Once Jenkins is installed, Click ***Finish***.

![jenkins15](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jenkins15.png)

## 8. Configuring Jenkins <a name="8"></a>

### Run Jenkins for the first time

Complete Jenkins Installation.

Open your web browser and type the URL http://localhost:8080. You should see the Jenkins initial setup screen.  

Navigate to “C:\ProgramData\Jenkins\ .jenkins\secrets\". Open the ***initialAdminPassword*** file using a text editor such as Notepad. 

Copy the password from the ***initialAdminPassword*** file and paste it in the "Administrator password" field and click "Continue" to proceed.

![jenkins9](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins9.png)

Click the "Install suggested plugins" button to install the most frequently used plugins. Wait for a while.

![jenkins10](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins10.png)

After Jenkins finishes installing the plugins, you should see the Create First Admin User page. Provide your username, password, email and click on the "Save and Continue" button.

![jenkins11](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins11.png)

Define your Jenkins URL and click on the "Save and Finish" button. 

![jenkins12](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins12.png)

Click the "Start using Jenkins" button.

![jenkins13](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins13.png)

Jenkins Welcome Dashboard.

![jenkins14](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/jenkins14.png)

### Connecting Jenkins to Github

**Create a Personal Access Token in GitHub**

In order for Jenkins to watch your GitHub projects, you will need to create a Personal Access Token in our GitHub account.

Visit GitHub and sign into your account. Click on your user icon in the upper-right hand corner and select Settings from the drop down menu.

On the page that follows, locate the Developer settings section on the left-hand menu and click Personal access tokens. Choose Tokens (classic).

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

![gh5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh5.png)

On the next page, click the arrow next to (global) across System (Stores from parent). In the box that appears, click Add credentials:

![gh6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh6.png)

Fill out all the fields same as below:

![gh7](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh7.png)

Click the "Create" button when you are finished.

![gh8](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh8.png)

Once you are done, restart Jenkins once.

![gh9](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/gh9.png)

## 9. Creating Jenkins Pipeline <a name="9"></a>

On the Jenkins dashboard, click on "New Item". 

![p0](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p0.png)

Enter an item name, for example, "devopsweb" and select the "Pipeline" project. Then click OK.

![p1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p1.png)

In the Configuration Dashboard, scroll down to the "Pipeline" section, and insert your code here. 

![p2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p2.png)

```sh
pipeline {
    
    agent any  

    stages {
        stage('Clone') {
            steps {
                git branch: 'master',
                    credentialsId: 'github_key',
                    url: 'https://github.com/vottri/DevOpsRepo.git'
            }
        }
        stage('Build') {
            steps {
                bat '''
                appcmd stop apppool "devopsweb"
                dotnet publish DevOpsWeb/DevOpsWeb.csproj -c Release -o C:/www/devopsweb
                
                '''
            }
        }
        stage('Clean') {
            steps {
                bat '''
                appcmd start apppool "devopsweb"
                '''
            }
            post {
                always {
                    cleanWs()
                }
            }
        }
    }
}
```
Components of Jenkins Pipeline:

 - The **pipeline** consists of all the instructions to build, test, and deliver software. It is the key component of a Jenkins Pipeline.

 - An **agent** is assigned to execute the pipeline on a node and allocate a workspace for the pipeline.

 - A **stage** is a block that has steps to build, test, and deploy the application. Stages are used to visualize the Jenkins Pipeline processes.

 - A **step** is a single task to be performed, for example, create a directory, run a docker image, delete a file, etc.

// Any available agent is getting assigned to the pipeline

// Get code from a GitHub repository
 
![p3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p3.png)
 
You can hover the cursor over the stages in "Stage View" section and choose "View Logs" to see detailed logs of every stages.
 
Logs from "Clone" Stage:
 
![p4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p4.png)
 
Logs from "Build" Stage:
 
![p5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p5.png)
 
Logs from "Clean" Stage:
 
![p6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p6.png)
 
Your website directory after Jenkins pipeline finishes running.
 
![p7](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p7.png)
 
You can also check your website in IIS Manager.
 
![p8](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p8.png)
 
Or simply view it by typing "localhost" in web browser.
 
![p9](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p9.png)
 
 
 
Visit GitHub and sign into your account. Modify your code and commit changes.
 
![p10](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p10.png)
 
Head over to Jenkins Dashboard and click "Build Now" to make Jenkins pipeline runs one more time.

![p11](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p11.png)
 
In your web browser, refreash the "localhost" page to view the changes.

![p12](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p12.png)

## 10. Publish your website and secure it with SSL <a name="10"></a>

Your web server (Azure VMs) already has an external IP Address due to it is being deployed on Azure Cloud. 

![p13](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p13.png)

You can test it by accessing your website over the Internet with the above IP Address.
 
![p14](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p14.png)

Register a Domain Name for your website and make sure it DNS record point to your public IP address.
 
![p15](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p15.png)
 
Modify your website hostname by editing its bindings in IIS Manager.

![p16](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p16.png)

Access your website using registered domain name.
 
![p17](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p17.png)


Extract the downloaded win-acme.v2 zipped files

![acme0](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/acme0.png)
 
Run wacs.exe (this requires administrator privileges).

Choose N in the main menu to create a new certificate with default settings.

Continue to answer the questions to determine the domain name that you want to include in the certificate. This can be derived from the bindings of an IIS site, or you can input them manually.

![acme1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/acme1.png)

A registration is created with the ACME server, if no existing one can be found. You will be asked to agree to its terms of service and to provide an email address that the administrators can use to contact you.

The program negotiates with ACME server to try and prove your ownership of the domain(s) that you want to create the certificate for. 

After the proof has been provided, the program gets the new certificate from the ACME server and updates or creates IIS bindings as required.

![acme2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/acme2.png)

After you are done with the script, type Q to quit.

Acces your website with HTTPS.

![p18](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p18.png)

Verify its certificate.

![p19](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/p19.png)
 
 
 
 
 


