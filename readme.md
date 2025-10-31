## Grafana Console for UberAgent data in Elasticsearch database

### Setup Procedure
1. Setup Elasticsearch following the Elasticsearch documentation.
2. Run the following PowerShell commands to create the UberAgent template, and the initial index.  Make sure that you run the second line before you setup UberAgent to send data to Elasticsearch, otherwise the @timedate field is created as text instead of date.
```
Invoke-RestMethod -Uri http://<url>:9200/_index_template/uberagent -Method Put -InFile "C:\temp\elasticsearch-uberagent.json" -ContentType "Application/json"

Invoke-RestMethod -Uri http://<url>:9200/uberagent -Method Put -ContentType "Application/json"
```
3. Setup Grafana following the Grafana documentation.
4. Create an Elasticsearch datasource pointing to your instance.
5. Import the Dashboards listed, adjust the data source in the Dashboard if it doesn't automatically connect.