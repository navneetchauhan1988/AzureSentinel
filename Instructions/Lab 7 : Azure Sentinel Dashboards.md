# Lab : Azure Sentinel Dashboards

Estimated Time: 45 minutes

Dashboards are a focused and organized view of your cloud resources in the Azure portal.
Use dashboards as a workspace where you can quickly launch tasks for day-to-day operations and monitor resources. 
Build custom dashboards based on projects, tasks, or user roles, for example.

## Exercise 1 : Creating Azure shared Dashboards

1. From the Azure portal menu, select **Dashboard**.

![image](https://user-images.githubusercontent.com/33748560/89714258-fbcecd00-d9ba-11ea-8b5b-a6aab75981a7.png)


2. Select **+New dashboard**.

3. Select the **My Dashboard** text in the dashboard label and enter a name that will help you easily identify the custom dashboard.

4. Select a tile and drag it to a new location on the grid to arrange your dashboard.

5. Select **Done customizing** in the page header to exit edit mode.

## Exercise 2 : Creating Azure Dashboard using Seninel Community

1. Open Azure Sentinel Page 

2. Select **Community** , click **Go to Azure Sentinel community**


![image](https://user-images.githubusercontent.com/33748560/89714549-143fe700-d9bd-11ea-9fd2-061d8ca28d88.png)



3. Open **Dashboards** folder in the github repository.

4. Open **Azure_AD_Audit_Logs.json** 

5. Click Edit button and Copy entire JSON code

![image](https://user-images.githubusercontent.com/33748560/89670794-66223780-d8ff-11ea-8812-8e2cd7f9c2b6.png)

6. Open a text editor , eg. notepad  ,  and paste  the content in text editor.

7. Replace the following value with actual values 

                      {Subscription_Id}
                      {Resource_Group}
                      {Workspace_Name}
                      
      (if required ask your instructor for assistance on above details.)
                      
8. Save the file with your_required_name.json 
                     
9 Switch to Azure Portal , 

10. From the Azure portal menu, select **Dashboard**.

![image](https://user-images.githubusercontent.com/33748560/89714258-fbcecd00-d9ba-11ea-8b5b-a6aab75981a7.png)

11. Select **Upload** button and choose the .json file saved in step 8 .

12. Repeat step 1 through 11 to create more dashboards.








Results: You have now completed this lab.


                                          
              


