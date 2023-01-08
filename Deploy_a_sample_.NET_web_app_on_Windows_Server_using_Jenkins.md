
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

Installing IIS Server

On Windows Server, go to Server Manager. Click on the "Add roles and features" on the dashboard. Click ***Next*** to proceed.

Select Role-based or feature-based installation, and then click ***Next***.

Select the server.

![iis1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis1.png)

Choose the "Web Server" option.

![iis2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis2.png)

Choose as below.

![iis3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis3.png)

Continue to proceed with below options.

![iis4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/iis4.png)

In the final screen, click the "Install" button to begin the installation. Once IIS has been installed, click "Close".

Configuring IIS Server

Open Windows Explorer. Create a new directory for your web site.

![web1](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web1.png)

In "Server Manager" Dashboard. Go to "Tools". Open "Internet Information Services Manager".

In IIS, you will have an initial site set up called "Default Web Site". We are not gonna use it.

Right-click "Default Web Site". Click "Edit Bindings". 

![web2](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web2.png)

When "Site Bindings" dialogue box appears, click "Edit". Change Port to 8088. Click OK.

![web3](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web3.png)

Creata a new website.

Right-click "Sites". Choose "Add Website".

![web4](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web4.png)

Fill in the required information as below. Then Click OK.

![web5](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web5.png)

![web6](https://raw.githubusercontent.com/vottri/CICD-pipeline-with-Jenkins/main/images1/web6.png)

## 4. Installing .NET SDK <a name="4"></a>

Install .NET SDK 6.0

![dotnet6](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet6.png)

![dotnet3](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet3.png)

Install ASP.NET Core Runtime 3.1 

![dotnet4](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/dotnet4.png)


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

Go to where you have downloaded the JDK application on your machine and double click the application. Click ***Next*** to start the installation.


***Next***.



Wait till the installation is completed and click ***Close***.

![jv1](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv1.png)


![jv2](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv2.png)


![jv3](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv3.png)


![jv4](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv4.png)

![jv5](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv5.png)
![jv6](https://github.com/vottri/CICD-pipeline-with-Jenkins/blob/main/images1/jv6.png)
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

Open your web browser and type the URL http://localhost:8080. You should see the Jenkins initial setup screen.  

Navigate to Open the ***initialAdminPassword*** file using a text editor such as Notepad. 

Copy the password from the ***initialAdminPassword*** file and paste it in the Administrator password field on the Unlock Jenkins page and click Continue to proceed.

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



## 8. Configuring Jenkins <a name="8"></a>

## 9. Creating Jenkins Pipeline <a name="9"></a>


## 10. domain and ssl <a name="10"></a>
