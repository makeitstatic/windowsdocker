# Use MS Windows image
FROM microsoft/windows

# Create temp folders
RUN New-Item -Path 'C:\\Scripts' -ItemType Directory

RUN New-Item -Path 'C:\\Jenkins' -ItemType Directory

# Fetch Jenkins Installation files, add also downloads
ADD https://ftp.halifax.rwth-aachen.de/jenkins/windows-stable/2.263.3/jenkins.msi C:/Jenkins

# Copy required demo files to container, copy only copies
COPY Scripts\HelloWorld.java c:\\Scripts\HelloWorld.java

# This is a script that installs chocolatey package manager without user prompt
COPY Scripts\ChocolateyInstallNonAdmin.ps1 c:\\Scripts\ChocolateyInstallNonAdmin.ps1
# sets the default shell
SHELL ["powershell"]

# Install Chocolatey
RUN Set-ExecutionPolicy Bypass -Scope Process -Force;

RUN c:\\Scripts\ChocolateyInstallNonAdmin.ps1

# Install Java with chocolatey manager
RUN choco install jdk8 -y  

RUN choco install adobereader

RUN choco install vscode
 
# Install IIS in powershell fashion, advantage of windows container
RUN -Command Install-WindowsFeature Web-Server

# Install Jenkins, msi installation silent install syntax
RUN ["msiexec.exe", "/i", "C:\\Jenkins\\jenkins.msi", "/qn"]

# Remove install files
RUN -Command Remove-Item c:/Jenkins - Recurse

# Compile Java class
RUN javac c:\\Scripts\HelloWorld.java

# Run Java script 
ENTRYPOINT java HelloWorld