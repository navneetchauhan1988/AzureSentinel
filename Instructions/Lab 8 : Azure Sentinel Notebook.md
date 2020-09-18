# Lab : Azure Sentinel Notebook

Estimated Time: 45 minutes


The Azure portal and all Azure Sentinel tools use a common API to access this data store. The same API is also available for external tools such as Jupyter notebooks and Python. 
While many common tasks can be carried out in the portal, Jupyter extends the scope of what you can do with this data. It combines full programmability with a huge collection of libraries for **machine learning, visualization, and data analysis.** 
These attributes make Jupyter a compelling tool for security investigation and hunting.

Jupyter experience into the Azure portal, making it easy for you to create and run notebooks to analyze your data.
The **Kqlmagic** library provides the glue that lets you take queries from Azure Sentinel and run them directly inside a notebook.
Several notebooks, developed by some of Microsoft's security analysts, are packaged with Azure Sentinel. 
Some of these notebooks are built for a specific scenario and can be used as-is. Others are intended as samples to illustrate techniques 
and features that you can copy or adapt for use in your own notebooks. 

Notebooks have two components:

* The browser-based interface where you enter and run queries and code, and where the results of the execution are displayed.

* A kernel that is responsible for parsing and executing the code itself.

In Azure Notebooks, by default, this kernel runs on Azure Free Cloud Compute and Storage. 
If your notebooks include complex machine learning models or visualizations, consider using more powerful,
dedicated compute resources such as **Data Science Virtual Machines (DSVM).** Notebooks in your account are kept private unless you choose to share them.

The Azure Sentinel notebooks use many popular Python libraries such as pandas, matplotlib, bokeh, and others. 
There are a great many other Python packages for you to choose from, covering areas such as:

Visualizations and graphics
Data processing and analysis
Statistics and numerical computing
Machine learning and deep learning

## Exercise 1 : Run a notebook from Azure Sentinel

1. From the Azure portal, navigate to **Azure Sentinel** > **Threat management** > **Notebooks**, where you can see notebooks that Azure Sentinel provides.

2. Select individual notebooks to read their descriptions, required data types, and data sources. For example:

![image](https://user-images.githubusercontent.com/33748560/89772994-aad8e900-db20-11ea-8f89-36ce9e5e4653.png)

3. Select first  notebook **A Getting Started Guide For Azure Sentinel Notebooks** and then click **Launch Notebook (Preview)** to clone and configure the notebook into a new Azure Notebooks project that connects to your Azure Sentinel workspace. When the process is complete, the notebook opens within Azure Notebooks for you to run.

4. Under AzureML workspace , click **create New 

![image](https://user-images.githubusercontent.com/33748560/93553606-0d7b9b00-f991-11ea-9fb6-014ad378aa4a.png)

5. Provide parameter settings ,  click **Review + Create** and click **Create

![image](https://user-images.githubusercontent.com/33748560/93553819-9f83a380-f991-11ea-8e8d-371b4abaadcd.png)

6. wait for the resource deployment , when completed , click **Go to Resource

![image](https://user-images.githubusercontent.com/33748560/93555290-2be29600-f993-11ea-8295-ca09c832b6bd.png)

7. On Machine Learning workspace , click **Launch Studio 

8. Select **Notebooks** on left

![image](https://user-images.githubusercontent.com/33748560/93555542-db1f6d00-f993-11ea-8dcc-61b92ba7d09f.png)

9. Click **Create** , **Create New File**

10. Provide a friendly name to your notebook and Select **file type** as Notebook.

11. Create Compute as displayed in below Screen Shot

![image](https://user-images.githubusercontent.com/33748560/93556403-49fdc580-f996-11ea-8935-902c8cf96eeb.png)

![image](https://user-images.githubusercontent.com/33748560/93556543-9812c900-f996-11ea-8057-2b68c9fefdc1.png)

12. Ensure you have necessary compute in Azure ML workspace

![image](https://user-images.githubusercontent.com/33748560/93556698-f770d900-f996-11ea-9399-1965e438225a.png)


The first thing you probably want to do, is to connect your Notebook with the Sentinel workspace.<br>
Click on your first cell. Notice that you can switch **cell type** in the Cell menu , to either Code, Markdown or Raw NBConvert. The default is code.<br><br>

Copy and paste the following in your cell and run  cell:

```python
!pip install Kqlmagic --no-cache-dir --upgrade
```


This will install KqlMagic, a library that will run KQL queries against a workspace.<br>
While having the cell selected, hit Ctrl+Enter, this will execute your cell content.

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/install-kqlmagic.png
)<br><br>

Since your Notebook is running in Azure, you will see that KqlMagic is actually already installed, this will not the case in a docker instance running locally. But it's a good practice to make sure you have the lastest version running.

:bulb: *Ctrl+Enter will execute the cell content, while typing "O" will clear the cell output*

#### Configure your workspace settings and connect
To connect to your Sentinel workspace, we need to provide your workspace settings. This can be configured through a Jupyter configuration file (recommended) or in the Notebook itself. For now we will configure it in the Notebook.<br>

:triangular_flag_on_post: *Your homework: figure out how you can get your workspace configuration settings from a config file*

1. Insert a new cell and add the following content:
```python
# Workspace connection variables
path = %env PATH
tenant_id = '<Your TenantId>'
subscription_id = '<Your SubscriptionId>'
resource_group = '<Your ResourceGroup>'
workspace_id = '<Your WorkspaceId>'
workspace_name = '<Your WorkspaceName>'
print('We are going to use the following Log Analytics Workspace: {}'.format(workspace_name))
```
2. Run the cell
3. Insert another cell and add the following:
```python
# Reload KqlMagic and connect to the workspace (requires )
%reload_ext Kqlmagic
%kql loganalytics://code;workspace=workspace_id;tenant=tenant_id
```
4. Run the cell<br><br>
:bulb: If you see an star in brackets like this **[*]** it means that the cell content is being executed 

5. Make sure you pay attention to the cell output and login into Azure:

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/login-workspace.png
)<br><br>

After a succesful Azure login, you are ready to run your first KQL query using a Jupyter Notebook!<br><br>
*Note: ignore any Javascript errors*

### Running a KQL query
**1. Insert a new cell, add the following and execute the cell:**
```python
%kql AzureActivity | summarize count() by Category
```
<br>
This would output something like this:

![image](https://user-images.githubusercontent.com/33748560/93557798-8bdc3b00-f999-11ea-8adb-3e794ea0fb0f.png)



:bulb: *Notice the following above*:<br>
***%kql** means that you are going to pass a KQL query on a single line. Using a double %% sign, means that you are going to use multi lines like the example in the following step*<br><br>

#### Kusto query
Execute the following to get the Azure Administrative Activites:
```python
%%kql
AzureActivity
| where Category == 'Administrative'
| limit 20









