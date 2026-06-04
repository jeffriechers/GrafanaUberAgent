# Grafana Consoles for UberAgent data in Azure Log Monitor and Elasticsearch database

This github is a repository for Grafana consoles to gather Citrix data from MSSQL DB queries, Azure Log Monitor, and from Elasticsearch with an UberAgent index.

Check the [Windows_install](./Windows_Install.md) for information on how to get started with Elasticsearch and Grafana setup in Windows.

Review [AzureLogMonitor_Import](./AzureLogMonitor_Import.md) for information on populating these Dashboards with your Azure Log Monitor connection info.

### UPDATES

**06-04-2026**


With microsoft setting an EOL of the HTTP API for Azure Log Monitor, Citrix has switched the preferred Azure Data Collector over the Event Hubs and Azure Data Explorer.  I have completely rebuilt my previous dashboards for this new data method, and have also created new dashboards around the ESA data collection as well.

[Screenshots for these new Azure Event Hub dashboards are available here.](./AzureEventHubReadme.md)

[Screenshots for the Elasticsearch dashboards are available here.](./Elasticsearchreadme.md)

[Screenshots for the Azure Log Monitor (deprecated on Sept 2026)](./AzureLogMonitorReadme.md)
