# Lab :  Automating threat responses in Azure Sentinel

Estimated Time: 45 minutes

A security playbook is a collection of procedures that can be run from Azure Sentinel in response to an alert. 
A security playbook can help automate and orchestrate your response, and can be run manually or set to run automatically when specific alerts are triggered. 
Security playbooks in Azure Sentinel are based on Azure Logic Apps, which means that you get all the power, customizability, 
and built-in templates of Logic Apps. Each playbook is created for the specific subscription you choose, but when you look at the Playbooks page, 
you will see all the playbooks across any selected subscriptions.

## Exercise 1: Set up automated threat responses in Azure Sentinel

### Task 1 : Create a security playbook

1.  Open the **Azure Sentinel dashboard**.

2.  Under **Configuration**, select **Playbooks**

3.  In the Azure Sentinel - Playbooks page, click **+Add Playbook** button.

![image](https://user-images.githubusercontent.com/33748560/89313574-4c31ec00-d696-11ea-8524-d92ed07bab85.png)


4. Logic App page will open , Provide details in Logic app parameters as below

![image](https://user-images.githubusercontent.com/33748560/89313952-b34fa080-d696-11ea-8232-935331685660.png)


5. Click **Review + Create** , Click **Create**

6. Click **Go to Resource**

7. On **Logic App Designer** blade , Select **Blank** template

![image](https://user-images.githubusercontent.com/33748560/89314592-7b952880-d697-11ea-8d95-ea5a224b26e0.png)

8. Search **Azure Sentinel**  and select the trigger as **When a response to an azure sentinel is triggered**

![image](https://user-images.githubusercontent.com/33748560/89315004-f52d1680-d697-11ea-8a46-8db2127824c1.png)

9. Click **Signin** and authenticate using azure service admin credentials.

10. Click **+New Step**

11. Under action , Select **Azure Sentinel** , and click **Alert : Get Incident**

![image](https://user-images.githubusercontent.com/33748560/89318207-1abc1f00-d69c-11ea-8cd0-f910524abcce.png)

12. Specify the dynamic values as below 

![image](https://user-images.githubusercontent.com/33748560/89318323-4212ec00-d69c-11ea-9427-80a6bb716deb.png)

13. Click  **+New Step**

14. Under Choose an action , Search for **Outlook.com**  , Select  **Send an email (V2)**

![image](https://user-images.githubusercontent.com/33748560/89316775-26a6e180-d69a-11ea-8f2a-2a663185cc0f.png)

15. Click **Signin**

16. Authenticate using your Microsoft account.

17. Draft an email with static and dynamic content  and click **Save**

![image](https://user-images.githubusercontent.com/33748560/89318974-26f4ac00-d69d-11ea-8a1a-fa4febd98ae8.png).

### Task 2: Associate Playbook with Analytics rule

1.  Open the **Azure Sentinel dashboard**.

2.  Click **Analytics**

3. Select the existing Analytics rule created in Lab 3 ,  **Brute force attack against Azure Porta** , Click **Edit**

4. Select **Automated Response** and Select the play book created in previous task , Click **Next** and Click **Save


![image](https://user-images.githubusercontent.com/33748560/89320146-bbabd980-d69e-11ea-9ed4-9da790e2bf32.png)

### Task 3 : Simulate risk to test analytics rule and detect threats 
     
  1. Simulate Brute force attack
  
               a.  Launch InPrivate window in browser and enter https://portal.azure.com/ in address bar 

               b. type work account which was created in step 1

               c. provide wrong password three times 

               d. provide correct password in fourth attempt.

               e. close the browser InPrivate window and reture back to azure sentinel page
   
   2. wait for 5-10  minutes.
   
   3. Open the **Azure Sentinel dashboard**.

   4.  Under **Configuration**, select **Playbooks**
   
   5. Click the Playbook you created in previous task
   
   6. Monitor Run history 
   
   ![image](https://user-images.githubusercontent.com/33748560/89322065-560d1c80-d6a1-11ea-8dd4-e0d4f5fa7212.png)


   7. Check your mailbox 
   
   ![image](https://user-images.githubusercontent.com/33748560/89322169-79d06280-d6a1-11ea-99d6-3e7316b918c2.png)


   
   
   Results: You have now completed this lab.















