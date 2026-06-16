#### CST8919 Lab 2: Building a Web App with Threat Detection using Azure Monitor and KQL

#### Code

#### learned during this lab
When working on this lab2, I learned how to deploy a Flask application to Azure App Service, enable diagnostic logging, send logs to a Log Analytics Workspace, and use Kusto Query Language to analyze application logs. 
I also learned how to create an Azure Monitor alert rule that sends an email notification when suspicious activity is detected.

#### KQL query
```
AppServiceConsoleLogs
| where TimeGenerated > ago(5m)
| where ResultDescription contains "LOGIN_FAILED"
| summarize FailedLoginCount = count() by bin(TimeGenerated, 5m)
```
##### Explanation:

This query is to searches the App Service console logs,  from the last 5 minutes. 
It will filter log messages that contain LOGIN_FAILED, after then, it will  count how many failed login attempts occurred for each 5 minutes 

##### Alert Rule Settings
```
Scope: Log Analytics Workspace
Signal: Custom log search
Query: KQL query above
Measure: Table rows
Threshold: Greater than 5
Aggregation granularity: 5 minutes
Frequency of evaluation: 1 minute
Severity: 2 or 3
Action Group: Email notification
```

#### YouTube video demo
##### App deployed
##### Log generation and inspection in Azure Monitor
##### KQL query usage
##### Alert configuration and triggering
