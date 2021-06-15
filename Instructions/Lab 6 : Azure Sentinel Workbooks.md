# Lab : Azure Sentinel Workbooks 

Estimated Time: 45 minutes

Workbooks provide a rich set of capabilities for visualizing your data. Workbooks can query data from multiple sources within Azure. Authors of workbooks can transform this data to provide insights into the availability, performance, usage, and overall health of the underlying components.

Once you have connected your data sources to Azure Sentinel, you can visualize and monitor the data using the Azure Sentinel adoption of Azure Monitor Workbooks, which provides versatility in creating custom dashboards.

## Lab scenario

You're a Security Operations Analyst working at a company that implemented Azure Sentinel. You must design workbooks with advanced visualizations.



## Exercise 1 : Use built-in workbooks

### Task 1 : Azure AD Audit Log Workbook

1. On Azure Sentinel Dashboard

2. Go to **Workbooks** and then select **Templates** to see the full list of Azure Sentinel built-in workbooks.

3. Select **Azure AD Audit Logs**

4. Click **View workbook** to see the template populated with your data.

![image](https://user-images.githubusercontent.com/33748560/89668323-307b4f80-d8fb-11ea-96bc-455929c3f8f1.png)

5. To edit the workbook, select **Save**, and then select the location where you want to save the json file for the template.

6. Select **View Saved workbook** ,   click the **Edit** button at the top. You can now edit the workbook and customize it according to your needs.

Refer to the below link for more details on customizing the workbook  
https://docs.microsoft.com/en-us/azure/azure-monitor/platform/workbooks-overview

7. After you make your changes, you can save the workbook.

8. You can also clone the workbook: Select **Edit** and then **Save as**, making sure to save it with another name, under the same subscription and resource group. These workbooks are displayed under the **My workbooks** tab.


## Exercise 2 : Create new workbook


### Task 1: Create a Workbook.

In this task, you will create a new workbook with advanced visualizations.

1. Select **Workbooks** in the Azure Sentinel portal.

2. Select **Add workbook**

3. Select **Edit**

#### Edit Header text:

4. Change *New workbook* to *My workbook*.

5. Select **Done Editing**.

6. Select **Edit** for the only visible graph.

7. Review the KQL statement that provides a union of counts across multiple tables.

8. Select the **Done Editing**.

9. Select **...** then select **Add**, then select **Add query**.

10. Enter *SecurityEvent*, then select **Run Query**.

11. Change the Timerange to **Last 3 days**.

12. Change the Visualization to different options and see the results.

13. Change the Visualization to **Time chart**.

14. Select **Style** from the Query tab.

15. Select the **Make this item a custom width** box.

16. Set the Percent width to **75** and Max Width to **75**.

17. Select **Advanced Settings** from the Query tab.

18. Select **Enable time range brushing** box. 

19. Enter *demoparam* for **Export selected time range as parameter**.

20. Select **Done Editing**.

21. On the displayed grid, click once, hold, and drag.  This will display a selected range.

22. Select **Add**, then **Add query**.

Enter the following KQL command for the query:

```
SecurityEvent
```

23. For Time Range, select **demoparam**.

24. Change the Visualization to **Grid**.

25. Select the **Style** tab.

26. Select **Make this item a custom width**.

27. Change percentage width to **25** and maximum width to **25**.

Done Editing for the Query

28. Select **Done Editing for the Workbook**.

29. Select **Save** and select **Save** again if prompted.

30. Select **Workbooks** in the Azure Sentinel portal.

31. Select the **My workbooks** tab.

32. Select the workbook you just created.

33. Select view saved workbook.

**Note:** Remember to try the timeslice by dragging on the grid.

## You have completed the lab.



