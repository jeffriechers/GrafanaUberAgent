## WinLogBeat Installation
WinLogBeat is an Elastic Agent that gets installed on Windows Servers and Desktops to capture Windows Event Logs and forward them to your Elasticsearch instance for aggregating and visualizing your event logs for easy searching of issues.

Make sure to run this AFTER setting up your Elasticsearch for UberAgent Data.

### Installation
Download the latest version of WinLogBeat from [WinLogBeat](https://www.elastic.co/downloads/beats/winlogbeat)

Extract the winlogbeat folder from the downloaded zip.  Rename it to winlogbeat and place it on your server's C:\Program Files directory.

Download the [winlogbeat.yml](.\winlogbeat.yml) file and modify the settings for your Elasticsearch server.  Also edit any of the Event Logs if you want to capture more or less data.

Place the modified winlogbeat.yml file into the c:\program files\winlogbeat directory, replacing the initial template.

Unblock the install-service-winlogbeat.ps1 and execute it on your machine.

Start the Winlogbeat service for it to start collecting data.

On your Grafana Dashboard, create a new Elasticsearch Data Connection to your Elasticsearch server and specify winlogbeat* for the index name.

Import the Windows Event Logs console from the Elasticsearch folder to your Grafana Console, and select the winlogbeat Data Connection you just created.

If you notice the variables are not refreshing, refresh the whole page.  This is a function of Grafana where it builds those variables on reload.

### Delete entries older than 30 days
When you first have machines launch Winlogbeat they will create all the necessary indexes, templates, and lifecycle management policies.

To age out records in Winlogbeat you can use the below PowerShell code to remove entries older than 30 days.

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
$body = @"
{
  "policy": {
    "phases": {
      "hot": {
        "actions": {}
      },
      "delete": {
        "min_age": "30d",
        "actions": {
          "delete": {}
        }
      }
    }
  }
}
"@

Invoke-RestMethod -Uri "http://<url>:9200/_ilm/policy/winlogbeat" -Method Put -ContentType "application/json" -Body $body -Credential $cred
```