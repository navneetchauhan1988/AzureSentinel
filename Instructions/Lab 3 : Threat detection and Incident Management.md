# Lab :  Threat detection and Incident Management

Estimated Time: 60 minutes

After you connected your data sources to Azure Sentinel, you can create custom Analytics rules that can search for 
specific criteria across your environment and generate incidents when the criteria are matched so that you can investigate them. 
This tutorial helps you create custom rules to detect threats with Azure Sentinel.

## Exercise 1: Create Analytics rule using builtin templates 

### Task 1 : Create  analytics rule for Azure Activity Data Source.

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

### Task 2 : Create  analytics rule for Azure Activity Directory source.

1. 1. On Azure Sentinel page , click **Analytics**

2. Select **Rule Templates**

3. Filter by  Data Source as **Azure Active Directory**

4. Select rule **Brute force attack against Azure Portal**

5. click **Create rule**

6. On General Page, Spend few minutes on rule parameters , click **Next**

7. On Set Rule Logic Page , update rule query with failureCountThreshold = 3 , set Run query every parameter to 5 Minutes, set Suppression
  On , Stop running query after alert is generated
  keep other parameters value as default , click **Next**
  
  ### Task 3 : Simulate risk to test analytics rule and detect threats
  
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

   
   




