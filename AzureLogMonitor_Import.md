## Grafana Azure Log Monitor Import process

You can directly import the consoles, and then manually change every dashboard to your Azure Log Monitor, but this is the easy process.

1. Create a Grafana connections to your Azure Log Monitor UberAgent Log.
2. Create a simple dashboard to that Data Source.
3. Open that dashboard in json view and look for the **"resources": [your connections sting will be here],** section. (For example  "resources": ["/subscriptions/11111111-1111-1111-1111-1111111111/resourceGroups/ResourceGroupName/providers/Microsoft.OperationalInsights/workspaces/uberagentlogname"],)
4. Open these .json files in your text editor of choice.
5. Do a find and replace for **"resources": [],** and replace it with your string from line 3.
6. Import the dashboards and start viewing data.
