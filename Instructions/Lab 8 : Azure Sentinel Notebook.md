# Lab : Azure Sentinel Notebook

Estimated Time: 45 minutes


The Azure portal and all Azure Sentinel tools use a common API to access this data store. The same API is also available for external tools such as Jupyter notebooks and Python. 
While many common tasks can be carried out in the portal, Jupyter extends the scope of what you can do with this data. It combines full programmability with a huge collection of libraries for machine learning, visualization, and data analysis. 
These attributes make Jupyter a compelling tool for security investigation and hunting.

Jupyter experience into the Azure portal, making it easy for you to create and run notebooks to analyze your data.
The Kqlmagic library provides the glue that lets you take queries from Azure Sentinel and run them directly inside a notebook.
Several notebooks, developed by some of Microsoft's security analysts, are packaged with Azure Sentinel. 
Some of these notebooks are built for a specific scenario and can be used as-is. Others are intended as samples to illustrate techniques 
and features that you can copy or adapt for use in your own notebooks. 

Notebooks have two components:

* The browser-based interface where you enter and run queries and code, and where the results of the execution are displayed.

* A kernel that is responsible for parsing and executing the code itself.

In Azure Notebooks, by default, this kernel runs on Azure Free Cloud Compute and Storage. 
If your notebooks include complex machine learning models or visualizations, consider using more powerful,
dedicated compute resources such as Data Science Virtual Machines (DSVM). Notebooks in your account are kept private unless you choose to share them.

The Azure Sentinel notebooks use many popular Python libraries such as pandas, matplotlib, bokeh, and others. 
There are a great many other Python packages for you to choose from, covering areas such as:

Visualizations and graphics
Data processing and analysis
Statistics and numerical computing
Machine learning and deep learning

## Exercise 1 : Run a notebook from Azure Sentinel

1. From the Azure portal, navigate to **Azure Sentinel** > **Threat management** > **Notebooks**, where you can see notebooks that Azure Sentinel provides.


