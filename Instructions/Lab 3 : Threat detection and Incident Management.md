# Lab :  Threat detection and Incident Management

Estimated Time: 60 minutes

After you connected your data sources to Azure Sentinel, you can create custom Analytics rules that can search for 
specific criteria across your environment and generate incidents when the criteria are matched so that you can investigate them. 
This tutorial helps you create custom rules to detect threats with Azure Sentinel.

## Exercise 1: Create Analytics rule using builtin templates 

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
