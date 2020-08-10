## Lab 1 -  Create a Data Science Virtual Machine (DSVM)
Every Jupyter Notebook needs to be hosted, either locally, or in Azure. In Azure you can use a shared service, or host your notebooks on your own VM.<br>
In this lab - for better performance - you are going to create a DSVM.<br><br>

1. Navigate to the Azure portal and create a new **Data Science VM for Linux (Ubuntu)**, with any instance details of your liking:<br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/create-dsvm.png
)<br><br>
This image contains JupyterHub and opens the required ports upon creation.
While the VM is being deployed, proceed to the next lab.


## Lab 2- Create your first Jupyter Notebook
1.	Navigate to https://notebooks.azure.com/ and login with your Corp credentials
2.	Click on My Projects and click on **New Project** and create your first project with any name:

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/create-project.png
)<br><br>

Now that you have created a project, let's add a Notebook.<br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/create-notebook.png
)<br><br>

## Lab 3 - Start your Notebook
Verify that your DSVM has deployed successfully and is up & running.<br>

Your NSG should contain a JupyterHub allow rule for TCP 8000.<br><br>

1. Start your new Notebook and select the **Direct Compute** option.
2. Configure the settings in the screen below based on your DSVM settings:
![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/configure-dsvm.png
)<br><br>

*Note:*<br>
If you are getting a message "Kernel not found", select Python 3.6 - AzureML:
![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/python3.6-kernel.png
)<br><br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%201%20-%20Creating%20a%20DSVM/images/notebook-running.png
)<br><br>

**Your Jupyter Project and Notebook has been created and your notebook is up & running.<br>
Proceed to the next lab, where the fun starts!**

## Lab 2 -  Building out your Jupyter Notebook
In the following exercises you will build up your Notebook from scratch. Feel free to go explore on your own, copy snippets from other Notebooks, or to skip some parts (although some have dependencies). This is all about getting your hands dirty with Jupyter Notebooks.<br>

My (personal) best learning experience is to start small, with snippets you understand, before cloning Notebooks. The following exercises are meant to do just that.<br><br> 

### Connecting your Notebook with the Sentinel workspace
The first thing you probably want to do, is to connect your Notebook with the Sentinel workspace.<br>
Click on your first cell. Notice that you can switch **cell type** in the Cell menu , to either Code, Markdown or Raw NBConvert. The default is code.<br><br>

Copy and paste the following in your cell:

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
%kql loganalytics://code;workspace=workspace_id;tenant=tenant_id;alias="<Your WorkspaceName>"
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
%kql SecurityAlert | summarize count() by ProductName
```
<br>
This would output something like this:

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/kql-query1.png
)<br><br>


:bulb: *Notice the following above*:<br>
***%kql** means that you are going to pass a KQL query on a single line. Using a double %% sign, means that you are going to use multi lines like the example in the following step*<br><br>

### Matching VM addresses with TOR and C2 addresses
In this exercise you will leverage ServiceMap Kusto data, which has outbound IP addresses.<br>
You will match these addresses with TOR and C2 data to hunt for IOC's.

#### Kusto query
Execute the following to get the ServiceMap addresses:
```python
%%kql
VMConnection
| where Direction == 'outbound'
| limit 20
```
Put the output in a dataframe:
```python
connections = _.to_dataframe()
```

Since you probably don't have a much, we are going to cheat a little bit and insert a row with a demo IP address:
```python
connections2 = pd.DataFrame({'DestinationIp': ['82.118.242.113'], 'Computer': ['ContosoDc']})
connections=connections.append(connections2)
connections
```
<br>

:grey_exclamation: **Make sure you see the inserted row!**

### Tor list retrieval
Now you are going to retrieve an external TOR list.<br>
First import the panda library:
```python
import pandas as pd
```

Now get the TOR list:
```python
torlist = pd.read_csv('https://www.dan.me.uk/torlist',header=0,names=["DestinationIp"])
```
Let's check if we got the TOR list allright:
```python
# Check if we have a solid Torlist, show only 5 rows
torlist.sample(5)
```
Now, you are going to check if we have a match (you should):
```python
# Check if we find a match (you should since we inserted a demo row)
connections.merge(torlist, on="DestinationIp")
```
You should see something like this:<br>

![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/torlist.png
)<br><br>

#### Assignment!
:triangular_flag_on_post: Use the concept to resolve addresses you already have with Whois<br><br>

I will get you started.<br><br>

Add the following new cells, which will import the Whois library and runs a test:
```python
#import Whois
from dns import reversename, resolver
from ipwhois import IPWhois
```
Run a test:
```python
    whois = IPWhois('167.220.152.151')
    whois_result = whois.lookup_whois()
    if whois_result:
        display(whois_result)
    else:
        print('No whois result')
```
<br>

:bulb: *Try the same with a different IP address*

### C2 demo
This optional section is based on <a href="https://techcommunity.microsoft.com/t5/Azure-Sentinel/Security-Investigation-with-Azure-Sentinel-and-Jupyter-Notebooks/ba-p/432921" target="_blank">Ian Hellen's blogpost</a> to retrieve C2 addresses and match those with your outbound IP addresses to check if we can find IOC's. It's a great read and to leverage in your own Notebooks.
<br><br>

This section will only show you how to get the information. Your mission, if you choose to accept it, is the cross check these C2's with your ip addresses to hunt for IOC's.
<br><br>

Add the following cells and execute them:
```python
# Imports
import sys
import warnings

MIN_REQ_PYTHON = (3,6)
if sys.version_info < MIN_REQ_PYTHON:
    print('Check the Kernel->Change Kernel menu and ensure that Python 3.6')
    print('or later is selected as the active kernel.')
    sys.exit("Python %s.%s or later is required.\n" % MIN_REQ_PYTHON)

import numpy as np
from IPython import get_ipython
from IPython.display import display, HTML, Markdown
import ipywidgets as widgets

import matplotlib.pyplot as plt
import seaborn as sns
sns.set()
import networkx as nx

import pandas as pd
pd.set_option('display.max_rows', 100)
pd.set_option('display.max_columns', 50)
pd.set_option('display.max_colwidth', 300)

import msticpy.sectools as sectools
import msticpy.nbtools as nbtools
import msticpy.nbtools.entityschema as entity
import msticpy.nbtools.kql as qry
import msticpy.nbtools.nbdisplay as nbdisp

# Some of our dependencies (networkx) still use deprecated Matplotlib
# APIs - we can't do anything about it so suppress them from view
from matplotlib import MatplotlibDeprecationWarning
warnings.simplefilter("ignore", category=MatplotlibDeprecationWarning)

WIDGET_DEFAULTS = {'layout': widgets.Layout(width='95%'),
                   'style': {'description_width': 'initial'}}
display(HTML(nbtools.util._TOGGLE_CODE_PREPARE_STR))

from collections import OrderedDict

# Create an observation collector list
from collections import namedtuple
Observation = namedtuple('Observation', ['caption', 'description', 'item', 'link'])
observation_list = OrderedDict()
def display_observation(observation):
    display(Markdown(f'### {observation.caption}'))
    display(Markdown(observation.description))
    display(Markdown(f'[Go to details](#{observation.link})'))
    display(observation.item)

def add_observation(observation):
    observation_list[observation.caption] = observation
```
<br>

```python
# This report could equally be an email or some other text that you want to retrieve IoCs from.
import requests
url = 'https://www.fireeye.com/blog/threat-research/2019/03/winrar-zero-day-abused-in-multiple-campaigns.html'
response = requests.get(url)
if response.status_code != 200:
    print('Url request failed')

# We want to extract IoCs from this report
# FireEye list domains and ips with the final dot obfuscated - possibly to deter people from doing what I'm doing here.
# My apologies to FireEye in advance
ip_iocs = str(response.content).replace('[.]', '.')
```
<br>

```python
from msticpy.sectools import IoCExtract
ioc_extr = IoCExtract()
``
<br>

```python
iocs_found = ioc_extr.extract(src=ip_iocs, ioc_types=['ipv4', 'url', 'dns', 'md5_hash', 'sha1_hash'])
if 'ipv4' in iocs_found:
    print('IPs in report')
    for item in iocs_found['ipv4']:
        print(f'\t{item}')
if 'url' in iocs_found:
    print('Urls in report')
    for item in (url for url in iocs_found['url'] if 'fireeye' not in url.lower()):
        print(f'\t{item}')
if 'md5_hash' in iocs_found:
    print('MD5 Hashes in report')
    for item in iocs_found['md5_hash']:
        print(f'\t{item}')
if 'dns' in iocs_found:
    print('Domains in report')
    for item in (dns for dns in iocs_found['dns'] if 'fireeye' not in dns.lower()):
        print(f'\t{item}')
```

<br>
Add an IP address to get a match and show the C2 list:

```python
c2_ips = list(iocs_found['ipv4'])
c2_ips.append('13.71.172.135')
c2_ips
```
You should see something like this:
![alt text](https://github.com/tianderturpijn/Mos-Eisley/blob/master/Lab%202/images/c2_found.png
)<br><br>
<br>

:triangular_flag_on_post: Assignment: <br>
Build a cell which will check for IOC's in your environment<br><br>

#### Happy Hunting!
