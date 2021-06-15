# Lab :  Create queries for Azure Sentinel using Kusto Query Language (KQL).

Estimated Time: 60 minutes

Kusto query is a read-only request to process data and return results.
The request is stated in plain text, using a data-flow model designed to make the syntax easy to read, author, and automate.
Kusto query plays a crucial role in creating Azure Sentinel  threat detection rules , hunting queries , notebook, workbooks and dashboards.

## Exercise 1: Using Most common operators in KQL


1. In the Azure portal, type **Azure Sentinel**. 

![image](https://user-images.githubusercontent.com/33748560/89098916-36f45d80-d409-11ea-9275-fa0c6f61111e.png)

2. Click on **Azure Sentinel**

3. Under General , Click on **Logs** 
![image](https://user-images.githubusercontent.com/33748560/89102678-2bb12a00-d429-11ea-9cc8-ef367ff89970.png)

### Task 1 : count : Returns the count of rows in the table

1.  Enter the below query in editor and click **Run**

          AzureActivity
          |count

2. Review the result in result pane.

### Task 2 : take Returns up to the specified number of rows of data.

1.  Enter the below query in editor and click **Run**

          AzureActivity
          |take 10

2. Review the result in result pane.

### Task 3 : project : Selects a subset of columns.
1.  Enter the below query in editor and click **Run**

            AzureActivity
            |project TimeGenerated,CategoryValue,Caller,ActivityStatusValue

2. Review the result in result pane.

### Task 4 : where : Filters a table to the subset of rows that satisfy a predicate.
1.  Enter the below query in editor and click **Run**

        AzureActivity
        |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
        |take  10 
        |project TimeGenerated,CategoryValue,Caller,ActivityStatusValue
        

2. Review the result in result pane.

### Task 5 : sort : Sort the rows of the input table into order by one or more columns.
1.  Enter the below query in editor and click **Run**

        AzureActivity
        |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
        |sort by ResourceGroup desc 
        |take  10 
        |project TimeGenerated,CategoryValue,Caller,ActivityStatusValue,ResourceGroup

2. Review the result in result pane.

### Task 6 : top: Returns the first N records sorted by the specified columns
1.  Enter the below query in editor and click **Run**

         AzureActivity
          |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
          |top 5 by ResourceGroup desc 
          |take  10 
          |project TimeGenerated,CategoryValue,Caller,ActivityStatusValue,ResourceGroup

2. Review the result in result pane.

### Task 7 : extend: create custom and calculated columns
1.  Enter the below query in editor and click **Run**

          AzureActivity
            |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
            |top 5 by ResourceGroup desc 
            |extend  User = Caller
            |take  10 
            |project TimeGenerated,CategoryValue,User,ActivityStatusValue,ResourceGroup


2. Review the result in result pane.

### Task 8 : summarize: Aggregates groups of rows.
1.  Enter the below query in editor and click **Run**

           AzureActivity
            |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
            |top 5 by ResourceGroup desc 
            |extend  User = Caller
            |summarize Events_By_User = count() by User

2. Review the result in result pane.

### Task 9 : render: Renders results as a graphical output.
1.  Enter the below query in editor and click **Run**

ColumnChart

       AzureActivity
              |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
              |top 5 by ResourceGroup desc 
              |extend  User = Caller
              |summarize Events_By_User = count() by User
              |render  columnchart 
              
              
TimeChart

                  AzureActivity
                  |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
                  |top 5 by ResourceGroup desc 
                  |extend  User = Caller
                  |summarize Events_By_User = count() by User
                  |render  timechart
              
BarChart

                 AzureActivity
                |where CategoryValue == "Administrative" and ActivityStatusValue == "Success"
                |top 5 by ResourceGroup desc 
                |extend  User = Caller
                |summarize Events_By_User = count() by User
                |render  barchart 
          
           


2. Review the result in result pane.

### Task 10 : let statement: use of the let statement to declare variables. In the Query Window. Enter the following statement and select **run**: 


```KQL
let timeOffset = 2d;
let discardEventStatus = "Started";
AzureActivity 
| where TimeGenerated > ago(timeOffset) 
| where ActivityStatusValue != discardEventStatus
```



















