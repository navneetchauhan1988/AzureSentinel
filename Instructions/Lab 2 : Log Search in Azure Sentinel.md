# Lab :  Performing Log Search using Kusto Query Language.

Estimated Time: 60 minutes

Kusto query is a read-only request to process data and return results.
The request is stated in plain text, using a data-flow model designed to make the syntax easy to read, author, and automate.
Kusto query plays a crucial role in creating Azure Sentinel  threat detection rules , hunting queries , notebook, workbooks and dashboards.

## Exercise 1: Azure Sentinel Log search 

1. In the Azure portal, type **Azure Sentinel**. 

![image](https://user-images.githubusercontent.com/33748560/89098916-36f45d80-d409-11ea-9275-fa0c6f61111e.png)

2. Click on **Azure Sentinel**

3. Under General , Click on **Logs** 

4. Enter the below query in editor and click **Run**

**AzureActivity
|where CategoryValue == "Administrative" and ActivityStatus == "Succeeded"
|take  10 
|project TimeGenerated,CategoryValue,Level,ResourceGroup,ActivityStatus**

5. Review the result in result pane.


![image](https://user-images.githubusercontent.com/33748560/89102678-2bb12a00-d429-11ea-9cc8-ef367ff89970.png)





