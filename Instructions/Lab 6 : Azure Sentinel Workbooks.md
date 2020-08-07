# Lab : Azure Sentinel WorkBooks 

Estimated Time: 45 minutes

Workbooks provide a rich set of capabilities for visualizing your data. Workbooks can query data from multiple sources within Azure. Authors of workbooks can transform this data to provide insights into the availability, performance, usage, and overall health of the underlying components.

Once you have connected your data sources to Azure Sentinel, you can visualize and monitor the data using the Azure Sentinel adoption of Azure Monitor Workbooks, which provides versatility in creating custom dashboards.


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

### Task 1 : Create an Azure AD workbook

1. Go to **Workbooks** and then select **+Add workbook** to create a new workbook from scratch.

2. To edit the workbook, select **Edit**, and then add **text**, **queries**, and **parameters** as necessary.

3. Click **Advanced Editor**

![image](https://user-images.githubusercontent.com/33748560/89669420-0cb90900-d8fd-11ea-99ed-4bf878d1c069.png)

4. Right click and open following  Workbook library in a new tab   :  https://github.com/microsoft/Application-Insights-Workbooks/tree/master/Workbooks 

5. Open **Azure Active Directory/SignIns/** folder in the repository 

6. Open **Signins.workbook** and click **edit button**

7. Select all and Copy  to clipboard by pressing **Ctrl+C** , 

8. Switch to Azure Sentinel workbook advanced editor page, and replace the entire code with the clipboard

9. Click **apply** and **Save**.

10. Repeat step 1 through 9 to create more workbooks.


