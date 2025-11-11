## Grafana Console for UberAgent data in Elasticsearch database

This github is a repository for Grafana consoles to gather Citrix data from MSSQL DB queries, and from Elasticsearch with an UberAgent index.  Check the [Windows_install](./Windows_Install.md) for information on how to get started with Elasticsearch and Grafana setup in Windows.

Import the Grafana Dashboards under MSSQL and Elasticsearch and point them to Datasources defined in your environment.  Then setup UberAgent to send data to your Elasticsearch instance and begin viewing data.

I will contine to add Dashboards to this console, and will add Azure Data locations in the future as well.

### UPDATES

11-11-2025
I have built a Windows Event Log Dashboard around the winlogbeat agent for Elasticsearch to consolidate all your event logs into an easily sortable, searchable table. [Read More Here](./WinLogBeat_Install.md)

11-10-2025
I added a Browser Usage and Browser Performance Dashboard to the Elasticsearch section.  These require the UberAgent browser plug-in to be deployed to the VDA.  Right now they detect Windows machines, but will be adding MACOS detection as well soon.
