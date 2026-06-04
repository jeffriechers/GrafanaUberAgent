# Grafana Consoles for UberAgent

This github is a repository for Grafana consoles to gather Citrix data from MSSQL DB queries, Azure Data Explorer, Elasticsearch, CSVs and more.

Check the [Windows_install](./Windows_Install.md) for information on how to get started with Elasticsearch and Grafana in Windows.

~~Review [AzureLogMonitor_Import](./AzureLogMonitor_Import.md) for information on populating the Azure Log Monitor Dashboards with your Azure Log Monitor connection info.~~  Soon to be deprecated.

### UPDATES

**06-04-2026**

With microsoft setting an EOL of the HTTP API for Azure Log Monitor, Citrix has switched the preferred Azure Data Collector over the Event Hubs and Azure Data Explorer.  I have completely rebuilt my previous dashboards for this new data method, and have also created new dashboards around the ESA data collection as well.

### What do these console look like?

[Screenshots for these new Azure Event Hub dashboards are available here.](./AzureEventHubReadme.md)

[Screenshots for the Elasticsearch dashboards are available here.](./Elasticsearchreadme.md)

[Screenshots for the Azure Log Monitor (deprecated on Sept 2026)](./AzureLogMonitorReadme.md)


### Installation Requirements for Azure Data Explorer

1. Grafana installed either in Docker, or installed natively.
2. Install these Grafana plugins. [yesoreyeram-infinity-datasource](https://grafana.com/grafana/plugins/yesoreyeram-infinity-datasource/) and [Grafana-azure-data-explorer-datasource](https://grafana.com/grafana/plugins/grafana-azure-data-explorer-datasource/)
3. Setup your Azure backend following the official Citrix documentation [here.](https://docs.citrix.com/en-us/uberagent/8-x/installation/backend/configuring-microsoft-azure-data-explorer-adx-event-hubs)
4. Create a connection to Azure Data Explorer named **grafana-azure-data-explorer-datasource**.
5. Edit the .json files under AzureEventHub, and replace **uberagenthomelab** with the name of your database in Azure.
6. Import the modified .json dashboard files and visualize your data.
