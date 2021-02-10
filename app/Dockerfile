# Use MS Windows image
FROM microsoft/windows

# Create temp folder
RUN New-Item -Path 'C:\\temp' -ItemType Directory

# Copy required files to container
COPY HelloWorld.java c:\\temp\HelloWorld.java
# This is a script that installs chocolatey package manager without user prompt
COPY ChocolateyInstallNonAdmin.ps1 c:\\temp\ChocolateyInstallNonAdmin.ps1

RUN powershell.exe

# Install Chocolatey
RUN Set-ExecutionPolicy Bypass -Scope Process -Force;

RUN c:\\temp\ChocolateyInstallNonAdmin.ps1

# Install Java with chocolatey manager
 RUN choco install jdk8 -y  

 RUN choco install adobereader

 RUN choco install googlechrome

 RUN choco install vscode


RUN ["c:/installers/ChromeStandaloneSetup64.exe", "/silent", "/install"]

# Compile Java class
RUN javac c:\\temp\HelloWorld.java

# Run Java script 
ENTRYPOINT java HelloWorld