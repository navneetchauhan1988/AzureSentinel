# Lab :  Hunting Threats in Azure Sentinel

Estimated Time: 30 minutes


If you're an investigator who wants to be proactive about looking for security threats, 
Azure Sentinel powerful hunting search and query tools to hunt for security threats across your organization's data sources.

## Exercise 1: Hunt for threats with Azure Sentinel.

1. In the Azure Sentinel portal, click **Hunting**.

2. When you open the **Hunting** page, all the hunting queries are displayed in a single table.
 The table lists all the queries written by Microsoft's team of security analysts as well as any additional query you created or modified.
 By saving a query to your favorites, the query automatically runs each time the **Hunting** page is accessed.

3. Click **Run query** in the hunting query details page to run any query without leaving the hunting page.

4. Perform a quick review of the underlying query in the query details pane or click View query result to open the query in Log Analytics. At the bottom, review      the matches for the query.

5. Click on the row and select **Add bookmark** to add the rows to be investigated - you can do this for anything that looks suspicious.

6. Then, go back to the main **Hunting** page and click the **Bookmarks** tab to see all the suspicious activities.

7. Select a bookmark and then click **Investigate** to open the investigation experience. You can filter the bookmarks. For example, if you're investigating a        campaign, you can create a tag for the campaign and then filter all the bookmarks based on the campaign.

8. After you discovered which hunting query provides high value insights into possible attacks, you can also create custom detection rules based on your query and    surface those insights as alerts to your security incident responders.

## Exercise 2: Create a new hunting query:

1. Click **New query** 

2. Fill in all the blank fields as below and click **Create**.

        Name: Granting permissions to account
        Description:   Shows the most prevalent users who grant access to others on azure resources and for each account 
                        their common source ip address. If an operation is not from this IP address it may be worthy of investigation.
        Custom query: 
                      let timeframe = 7d;
                      AzureActivity
                      | where TimeGenerated >= ago(timeframe)
                      | where OperationName == "Create role assignment"
                      | where ActivityStatus == "Succeeded" 
                      | project Caller, CallerIpAddress
                      | evaluate basket()
                      | extend AccountCustomEntity = Caller, IPCustomEntity = CallerIpAddress
                      
       tactics:
                    - Persistence
                    - PrivilegeEscalation
                    
                    
### Create new hunting queries using Sentinel Community.

1. Create few hunting queries , run , and investigate. 

















