# Lab : Azure Sentinel watchlist

Estimated Time: 30 minutes

Azure Sentinel watchlists enable the collection of data from external data sources for correlation with the events in your Azure Sentinel environment. 
Once created, you can use watchlists in your search, detection rules, threat hunting, and response playbooks. 
Watchlists are stored in your Azure Sentinel workspace as name-value pairs and are cached for optimal query performance and low latency.

## Lab scenario

You're a Security Operations Analyst working at a company that implemented Azure Sentinel. You must create watchlist based on the Indicator of Compromise (IoC) provided.
In this scenario we will pretend a valid IPAddress as an IoC






## Exercise 1 : Add a CSV in watchlist

## Task 1: Note  IP Address  to simulate as an IoC

1. In Azure Sentinel , select **Logs**

2. In Query editor , type **AzureActivity**

3. Note the IPAddress under **CallerIPAddress** Field.

## Task 2 : Create and save a csv file

1. Create a csv file with Netwok and IPAddress fields 

2. Replace the IPAddress with one you recorded in previous task.

3. Save the CSV File.

## Task 3 : Add the csv file 

1. In Azure Sentinel , Select **Watchlist** , and click **+Add new

2. On the General page, provide the **name**, **description**, and **alias** for the watchlist, and then select **Next: Source.
 
3. On the Source page, select the dataset type (currently only CSV is available), enter the number of lines before the header row in your data file, and then choose a file to upload in one of two ways:

  Click the Browse for files link in the Upload file box and select your data file to upload.
  Drag and drop your data file onto the Upload file box.
  You will see a preview of the first 50 rows of results in the wizard screen.

4. In the **SearchKey** field, enter the name of a column in your watchlist that you expect to use as a join with other data or a frequent object of searches. For example, if your server watchlist contains server names and their respective IP addresses, 
   and you expect to use the IP addresses often for search or joins, use the **IPAddress** column as the SearchKey.

5. Select **Next: Review and Create**.

6. A notification appears once the watchlist is created.

## Task 4 : Use watchlists in queries

1. In Azure Sentinel , select **Logs**

2. ener the below query and run

```
//Watchlist as a variable
let watchlist = (_GetWatchlist('Test') | project IPAddress);
AzureActivity
| where CallerIpAddress in (watchlist)
```












Results: You have now completed this lab.


                                          
              


