# Lab :  Threat detection and Incident Management

Estimated Time: 60 minutes

After you connected your data sources to Azure Sentinel, you can create custom Analytics rules that can search for 
specific criteria across your environment and generate incidents when the criteria are matched so that you can investigate them. 
This tutorial helps you create custom rules to detect threats with Azure Sentinel.

## Exercise 1: Create Analytics rule definitions. 

### Task 1 : Create  analytics rule for Azure Activity Data Source using rule templates.

1. On Azure Sentinel page , click **Analytics**

2. Select **Rule Templates**

3. Filter by  Data Source as **Azure Activity**

![image](https://user-images.githubusercontent.com/33748560/89113789-f6412680-d492-11ea-8327-2d896be9b8d0.png)


4. Select rule **Suspicious granting of permissions to an account**

5. click **Create rule**

6. On General Page, Spend few minutes on rule parameters , click **Next**
   
   Few Common tactics are as below 
   
   ![image](https://user-images.githubusercontent.com/33748560/89113759-a4000580-d492-11ea-80ec-5016b1ac4d98.png)

    find more details on https://attack.mitre.org/tactics/enterprise/

7. On Set Rule Logic Page , keep the parameters value as default , click **Next**

8. On Incident Settings , keep the paramters value as default , click **Next**

9. On Automated Response , click **Next**

10 On Review and create , click **create**

11. Spend few minutes to review other Azure Activity rule templates as well and create few rules by repeating step 5 to 10.

### Task 2 : Create  analytics rule for Azure Activity Directory source using rule templates.

1. On Azure Sentinel page , click **Analytics**

2. Select **Rule Templates**

3. Filter by  Data Source as **Azure Active Directory**

4. Select rule **Brute force attack against Azure Portal**

5. click **Create rule**

6. On General Page, Spend few minutes on rule parameters , click **Next**

7. On Set Rule Logic Page , update rule query with failureCountThreshold = 3 , set Run query every parameter to 5 Minutes, set Suppression
  On , Stop running query after alert is generated
  keep other parameters value as default , click **Next**
  
8. On Incident Settings , keep the paramters value as default , click **Next**
9. On Automated Response , click **Next**

10 On Review and create , click **create**
  
  ### Task 3  : Create Custom analytics rule definition.
  
 1. In the Azure portal under , select **Analytics**.

 2. In the top menu bar, select **+Create** and select **Scheduled query rule**. This opens the Analytics rule wizard.
 
 3. In the General tab, Configure parameter as below 
 
             a. Name - GitHub Signin Burst from Multiple Locations.
             b. Description -This alerts when there Signin burst from multiple locations in GitHub (AAD SSO).
             c. Tactics - CredentialAccess,
             d. Severity - Medium
             e. Status - Enabled 
    
 4. click  **Set rule logic** 
 
 5. Enter the below query in **Rule Query**
 

 let RunTime = 1h;
  SigninLogs
  | where TimeGenerated > ago(RunTime)
  | where AppDisplayName == "GitHub.com"
  | where ResultType == 0
  | summarize CountOfLocations = dcount(Location), Locations = make_set(Location) by User = Identity
  | where CountOfLocations > 1
  //| extend AccountCustomEntity = UserPrincipalName, IPCustomEntity = IPAddress
  
  6. click **Next**
  
  7. On Incident Settings , keep the paramters value as default , click **Next**
  8. On Automated Response , click **Next**

  9.  On Review and create , click **create**
  
  
  
  
  ### Task 4 : Simulate risk to test analytics rule and detect threats 
  
  1. Create a User account in azure active directory 
  
  Note : If you are new to Azure AD management , then follow below link 
   
   https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/add-users-azure-active-directory
   
  2. Simulate Brute force attack
  
               a.  Launch InPrivate window in browser and enter https://portal.azure.com/ in address bar 

               b. type work account which was created in step 1

               c. provide wrong password three times 

               d. provide correct password in fourth attempt.

               e. close the browser InPrivate window and reture back to azure sentinel page
   
   3. wait for 5 minutes, 
   
   4. after 5 minutes click **Incidents** under Threat management in azure sentinel.
   
   5. click **Refresh** , there should be an Incident.
   
   ![image](https://user-images.githubusercontent.com/33748560/89115145-3e1b7a00-d4a2-11ea-98bb-5e131525354e.png)
   
  
    
  
      
      
   ## Exercise 2: Incident Management in Azure Sentinel
   
An incident can include multiple alerts. It's an aggregation of all the relevant evidence for a specific investigation. An incident is created based on analytic rules that you created in the Analytics page. The properties related to the alerts, such as severity, and status, are set at the incident level. After you let Azure Sentinel know what kinds of threats you're looking for and how to find them, you can monitor detected threats by investigating incidents.

   ### Task 1
   
   1. Select **Incidents** 
   
   ![image](https://user-images.githubusercontent.com/33748560/89115145-3e1b7a00-d4a2-11ea-98bb-5e131525354e.png)
   
   2. Using criterian filter you can filter the incidents as needed, for example by status or severity
   
   3. select a specific incident
   
   4. If you're actively investigating an incident, it's a good idea to set the incident's status to **Active** until you close it.

   5. Incidents can be assigned to a specific user. For each incident you can assign an owner, by setting the Incident owner field. 
      All incidents start as **unassigned**. You can also add comments so that other analysts will be able to understand what you investigated and what your             concerns are around the incident.
   
   6. select **View full details** for more details on incident
   
   7. In the **Alerts** tab, review the alert itself
   
   8. To drill down even further into the incident, select the number of **Events**
   
   9. Select  **Entities** tab, where you see all the entities that you mapped in alert rule definition.
   
   ### Task 3 : Use the investigation graph to deep dive
   
   1. Select an **incident**, then select **Investigate**. This takes you to the investigation graph.
   
   ![image](https://user-images.githubusercontent.com/33748560/89115476-3a89f200-d4a6-11ea-9743-976da3fe15ca.png)
    
   2. Select an entity to open the **Entities** pane so you can review information on that entity.
   
   3. Expand investigation by hovering over each entity to reveal a list of questions that was designed by our security experts and analysts per entity type          to deepen your investigation. This is called exploration queries
   
   4. For example, on a computer you can request related alerts. If you select an exploration query, the resulting entitles are added back to the graph. In this          example, selecting Related alerts returned the following alerts into the graph
   
   ![image](https://user-images.githubusercontent.com/33748560/89115549-1ed31b80-d4a7-11ea-8ef7-9d139968e084.png)

   5. For each exploration query, you can select the option to open the raw event results and the query used in Log Analytics, by selecting Events>.

   6. In order to understand the incident, the graph gives you a parallel timeline.
   
   7. Once you have resolved a particular incident (for example, when your investigation has reached its conclusion), you should set the incident’s status to              Closed. When you do so, you will be asked to classify the incident by specifying the reason you are closing it. This step is mandatory. Click Select                classification and choose one of the following from the drop-down list:

      True Positive - suspicious activity
      Benign Positive - suspicious but expected
      False Positive - incorrect alert logic
      False Positive - incorrect data
      Undetermined
   
   




