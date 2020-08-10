# Optional Lab
## Running a local docker container to host your Jupyter Notebook

This lab provides you the basic steps to leverage a local docker container which will run your Jupyter Notebook locally. This has a benefit that it runs fast and you have all your potential confidential data local.

#### Requirements
1. Before continuing, make sure that you have configured your computer with Hyper-V and that you have enough local resources available.<br>
2. In you Azure Notebooks environment, download your Notebook locally, so that you can import it later.

### Docker installation steps.
1. Navigate to <a href="https://hub.docker.com/r/jupyter/scipy-notebook/" target="_blank">https://hub.docker.com/r/jupyter/scipy-notebook/</a>
2. Download what you need
3. Open PowerShell
4. Verify your docker version by executing in PowerShell:
```powershell
docker version
```
5. Download docker Jupyter (execute in PowerShell):
```powershell
docker pull jupyter/scipy-notebook
```
6. Start you Jupyter Notebook (execute in PowerShell):
```powershell
docker run -p 8888:8888 jupyter/scipy-notebook
```
7. When you start your Jupyter instance, you will get your token in the output confirmation message, copy the connection string, similar like the following:
```powershell
http://127.0.0.1:8888/?token=67314026283a297c1dbc355a03ad370b0a097005e07f2f88
```
8. Open a browser and navigate to your Jupyter instance by pasting in the http string you have copied in the previous step

### Importing a Notebook
In your Jupyter screen, click on import and import and run your Notebook.<br>

#### Happy Hunting!





