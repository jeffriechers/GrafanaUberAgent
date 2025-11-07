## Downloads
1. Get the latest version of Elasticsearch for Windows.  https://www.elastic.co/downloads/elasticsearch
2. Get the latest version of Grafana for Windows. https://grafana.com/grafana/download?platform=windows


## Install Process
### Elasticsearch install
Extract the download elasticsearch version to c:\

In the elasticsearch\bin directory launch elasticsearch.bat

Capture the elastic user password generated during the install

Run the following powershell lines on the server to open the firewall ports for elasticsearch and grafana.
```
netsh advfirewall firewall add rule name="Elasticsearch" dir=in localport="9200"  protocol=TCP action=allow
netsh advfirewall firewall add rule name="Grafana" dir=in localport="3000"  protocol=TCP action=allow
```
Connect to the server on https://&lt;url&gt;:9200.  Login with elastic for the username, and the password you got from the console screen to validate it is working correctly.

Close the console window to shutdown Elasticsearch

### Password reset
If you want to change the password, or forget the elastic password, run the following command on the elasticsearch server to generate it.
```
.\bin\elasticsearch-reset-password -i -u elastic
```

### Service Registration
Run the following command to install the Elasticsearch service
```
.\bin\elasticsearch-service.bat install
```
Once the install is completed, then start the service with the following command.
```
.\bin\elasticsearch-service.bat start
```
If you need to modify the configuration of the service, you can run the following command.
```
.\bin\elasticsearch-service.bat manager
```

### UberAgent Index creation
Place the elasticsearch-uberagent.json into the c:\temp\ directory on your machine.  This is available from Citrix directly, or from my github repository

Modify the following PowerShell command uri strings, change the "&lt;url&gt;" item with the hostname of your elasticsearch server.

The commands before the $cred section is to allow PowerShell to accept the self-signed certs on the Elasticsearch instance.
```
Add-Type @"
using System.Net;
using System.Security.Cryptography.X509Certificates;

public class TrustAllCertsPolicy : ICertificatePolicy {
    public bool CheckValidationResult(
        ServicePoint srvPoint, X509Certificate certificate,
        WebRequest request, int certificateProblem) {
        return true;
    }
}
"@

[System.Net.ServicePointManager]::CertificatePolicy = New-Object TrustAllCertsPolicy

$cred = Get-Credential  # Prompts for username/password
Invoke-RestMethod -Uri https://<url>:9200/_index_template/uberagent -Method Put -InFile "C:\temp\elasticsearch-uberagent.json" -ContentType "Application/json" -Credential $cred

Invoke-RestMethod -Uri https://<url>:9200/uberagent -Method Put -ContentType "Application/json" -Credential $cred
```

### Grafana Setup
Install the downloaded version, ensure you have run as service selected along with Grafana Enterprise

Access the Grafana console on http://&lt;url&gt;:3000

Login with admin for the username and password

Choose a new password for the admin account

Click on Connections -> Data sources -> Add data source

Choose elasticsearch, and place the url to the server.  If running on the same box, you can use localhost.

Choose basic authentication, and enter your elastic username and password.  

If using self-signed certs on elasticsearch, check the Skip TLS certificate validation option

Click Save & Test at the bottom of the screen

### Dashboard Imports
Click on Dashboards -> Click the New Drop Down -> Select Import

Import the Dashboards downloaded from Github, select the elasticsearch Data Source you created earlier.

Click Import

Repeat for each Dashboard you want to deploy.