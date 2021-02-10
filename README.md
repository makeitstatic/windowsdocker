# windowsdocker
Windows docker file that builds a windows image and auto installs some apps.

Navigate to app folder.

docker build -t jenkinsetc .

docker run -it jenkinsetc powershell

password file: c:\Program Files (x86)\Jenkins\secrets\initialAdminPassword