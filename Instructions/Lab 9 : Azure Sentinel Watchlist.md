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
 ![Screen Shot 2021-06-17 at 10 07 50 PM](https://user-images.githubusercontent.com/33748560/122443288-0f749800-cfbd-11eb-9e84-bea42cf7be55.png)

## Task 2 : Create and save a csv file

1. Create a csv file with Netwok and IPAddress fields 

2. Replace the IPAddress with one you recorded in previous task.

![Screen Shot 2021-06-17 at 10 25 09 PM](https://user-images.githubusercontent.com/33748560/122443671-6f6b3e80-cfbd-11eb-9bcb-0d108ae94158.png)

3. Save the CSV File.

## Task 3 : Add the csv file 

1. In Azure Sentinel , Select **Watchlist** , and click **+Add new

![Screen Shot 2021-06-17 at 10 12 29 PM](https://user-images.githubusercontent.com/33748560/122443952-b35e4380-cfbd-11eb-93f1-842a4ffbe7ad.png)

2. On the General page, provide the **name**, **description**, and **alias** for the watchlist, and then select **Next: Source.


![Screen Shot 2021-06-17 at 10 17 11 PM](https://user-images.githubusercontent.com/33748560/122444081-d38e0280-cfbd-11eb-88b7-b0263fae876f.png)


 
3. On the Source page, select the dataset type (currently only CSV is available), enter the number of lines before the header row in your data file, and then choose a file to upload in one of two ways:

  Click the Browse for files link in the Upload file box and select your data file to upload.
  Drag and drop your data file onto the Upload file box.
  You will see a preview of the first 50 rows of results in the wizard screen.

4. In the **SearchKey** field, enter the name of a column in your watchlist that you expect to use as a join with other data or a frequent object of searches. For example, if your server watchlist contains server names and their respective IP addresses, 
   and you expect to use the IP addresses often for search or joins, use the **IPAddress** column as the SearchKey.
   
   ![Screen Shot 2021-06-17 at 10 17 50 PM](https://user-images.githubusercontent.com/33748560/122444221-f5878500-cfbd-11eb-8250-a0d9c326a82d.png)


5. Select **Next: Review and Create**.

![Screen Shot 2021-06-17 at 10 19 58 PM](https://user-images.githubusercontent.com/33748560/122444382-1bad2500-cfbe-11eb-8e0e-1e9d31f20d21.png)


6. A notification appears once the watchlist is created.

## Task 4 : Use watchlists in queries

1. In Azure Sentinel , select **Logs**

2. Access watch list , Ener the below query, replace **Test** with watchlist name you provided in previous exercise and run

```
_GetWatchlist('Test')
```

3. Find events in sentinel workspace based on the provided IoC

4. **Approach A** : Ener the below query, replace **Test** with watchlist name you provided in previous exercise and run

```
//Watchlist as a variable
let watchlist = (_GetWatchlist('Test') | project IPAddress);
AzureActivity
| where CallerIpAddress in (watchlist)
```


![Screen Shot 2021-06-17 at 10 27 38 PM](https://user-images.githubusercontent.com/33748560/122444494-3b444d80-cfbe-11eb-8a80-69e7864f3347.png)


5. **Approach B** : Ener the below query, replace **Test** with watchlist name you provided in previous exercise and run

```
//Watchlist inline with the query
//Use SearchKey for the best performance
AzureActivity
| where CallerIpAddress  in ( 
    (_GetWatchlist('Test')
    | project SearchKey)
)

```

![Screen Shot 2021-06-17 at 10 27 38 PM](https://user-images.githubusercontent.com/33748560/122444494-3b444d80-cfbe-11eb-8a80-69e7864f3347.png)












Results: You have now completed this lab.


                                          
              


