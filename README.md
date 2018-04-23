![](notebooks/assets/solutions-microsoft-logo-small.png)
<img src="notebooks/assets/ai.jpg" style="height:200px;float:right;vertical-align:text-top">

**Course Design Notes - remove after course Charlie-Lock:**

  -  Useful
  -  High Production Value
  -  Deep Learning with GPU (Keras often just knows, package dependency for TensorFlow - Check)
  -  Scale-out
  -  Deploy to IoT
  -  Supporting material can be found here: https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3 
  
**TODO:**
  - Convert lab notebooks to these notebooks *(complete)*
  - Change readme.md file to have the pre-reqs *(complete, now testing)*
  - Convert experiment to Linux DSVM
  - Convert tensorflow code to GPU-enabled
  - Include IoT as target
  - Deploy and test
  - Find/create location for data source files
  - Edit/check pre-reqs and setup - attribute the original
  - If the "Answer Key" is needed, make it, if not, remove reference in the first notebook.
  - Clean up files and directories for consistency, layout, person, and tense

## Artificial Intelligence on IaaS++

#### From the Microsoft Cloud and AI Team

This workshop leads you through a series of [Jupyter Notebooks](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html) that explain how to use the Microsoft Azure Data Science Virtual Machine (DSVM) and the Team Data Science Process (TDSP) to create Data Science and AI solutions. These solutions can be deployed in a variety of ways, leveraging Infrastructure-as-a-Service (IaaS) through Platform-as-a-Service (PaaS) environments, and a mixture of both based on requirements. 

The material for this workshop is intended for a Data Scientist familiar with Machine Learning, Python and R programming, Artificial Intelligence application development, and a professional backgound in team software development with methodologies such as Agile. [If any of these topics are new to you, we have a learning path here that you can follow to bring you up to speed before you start this workshop](https://github.com/Azure/learnAnalytics-CreatingSolutionswiththeTeamDataScienceProcess/blob/master/Instructions/Learning%20Path%20-%20Creating%20Solutions%20with%20the%20Team%20Data%20Science%20Process.md).

*This material draws from a [previous example](https://docs.microsoft.com/en-us/azure/machine-learning/desktop-workbench/scenario-deep-learning-for-predictive-maintenance), which draws from [yet another example](https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3).* 
    
<p style="border-bottom: 3px solid lightgrey;"></p>

### Prepare The Project - System Setup and Configuration

The following labs will guide you through setting up an account, a DSVM, and the Azure Machine Learning workspaces and other elements needed to create your solution. You'll also download the Project Plan for your solution for your team. 

<img src="notebooks/assets/dothings.jpg" style="height:100px;float:right;vertical-align:text-top">

In Phase One of this Workshop, you'll learn more about how to discover the questions that need an answer, information about the data sources you require, a determination of the algorithms and other parts of an experiment, creating a trained model, operationalizing the solution so that a customer can access it, and how to close out the project with the customer along with any model retraining that is needed. Before you begin these phases, you'll need to set up your environment to perform each of these steps. 

<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.0 - Set up an Microsoft Azure Account

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">

For experimentation and model management, we'll use the Microsoft Azure platform. There are four choices for setting up a Microsoft Azure account:

1. You can use a Free Subscription - [The process for setting that up is here](https://azure.microsoft.com/en-us/free/)
2. You can use a Microsoft Developer Network (MSDN) account - [The process for setting that up is here](https://azure.microsoft.com/en-us/pricing/member-offers/credit-for-visual-studio-subscribers/)
3. You can use a Corporate account - See your corporate person in charge of Azure accounts to see if you are able to create a Virtual Machine and other assets on your company subscription
4. If you are taking this workshop in an on-premises training class, your trainer  may provide an Azure Account login for you - Ask your training instructor for instructions for a login

*Once you have an Azure account login, open the Microsoft Azure Portal and continue to the next lab.*

<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.1  - Set up the Azure Data Science Virtual Machine

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">

Instructions:
1. [Open this page](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/provision-deep-learning-dsvm) and perform the steps to set up a **Linux** DSVM, with a **Password** rather than an SSH set of Keys.
2. Follow the instructions for that section, choosing **NC6 Standard** as the size of the DSVM
3. Complete the creation of the DSVM, and note the name, connection information and password for your system.

*(Note: You do not need to configure an X2Go client unless you want to - it is not required for the course)*

<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.2 - Log in to the DSVM and Update the System

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">

Instructions:
1. On your local system, open CMD on Windows or a Terminal Window on Linux. 
2. Type the following commands:

`sudo apt-get update`

(You will be prompted for the password you set in the Portal when you created the VM)

`sudo apt-get upgrade`

Allow the process to complete.

#### Lab verification
<p><img style="float: left; margin: 0px 15px 15px 0px;" src="./assets/checkbox.png">Commands complete successfully.</p> 
 
<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.3 - Create a Model Management Account

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">

Instructions:
1.  On your DSVM terminal connection, type the following commands:

`az login`

2. You will be given instructions for a web page and code to authorize the connection. Perform those actions. You will be given a login panel, use the Azure Account you started with for this Workshop.

3. Next, create an Azure Resource Group to hold all of the assets for this workshop with the following commands, entering the same region (which you can find in the Azure Portal) where you created your DSVM:
 
`az group create --name gpurg --location <ACCOUNT_REGION>`

*Note: You can find the correct text for the `<ACCOUNT_REGION>` using the command:*

`az account list-locations`

4. Now create a Model Management service in your Microsoft Azure account, called `gpumodelmanagement`. (You only need to do this once for any models you would like to deploy.) You will need to supply an **ACCOUNT_REGION** as before from your Azure account. The remaining defaults are acceptable. Run the following code:

`az ml account modelmanagement create --location <ACCOUNT_REGION> --resource-group gpurg --name gpumodelmanagement`

*Note: If you get an error involving the region, read the error message carefully and select a region that is listed.*

*Note: If you get a `ResourceGroupNotFound` error, you may need to set the correct subscription. This is typically only an issue if your Azure login connects to multiple subscritpions.*

`az account set -s '<subscription name>'`

You can find the `subscription name` or `subscription id` through the (https://portal.azure.com) under the resource group you'd like to use. 


#### Lab verification
<p><img style="float: left; margin: 0px 15px 15px 0px;" src="./assets/checkbox.png">Complete the steps that follow:</p>

1. Show the currently active environment:

`az ml env show`

2. You should get a message that the compute environment is not set. If so, activate the environment with your model management context (created above): 

`az ml env setup --location <ACCOUNT_REGION> --resource-group gpurg --name gpumodelmanagement`

...using the same `<ACCOUNT_REGION>` and `<RESOURCE_GROUP>` from the previous section. It will take a few minutes for this to complete. You can check the status with the command:

`az ml env show` 

3. Then set the current environment:

`az ml env set --resource-group gpurg --cluster-name gpumodelmanagement`

*Note: if you get an error that it is not complete, wait a few minutes and re-run the command.*

3.  When that command completes successfully, check that the environment is now set:

`az ml env show` 
 
<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.4 - Clone the Workshop's Jupyter Notebooks

< TODO: Change to Linux >

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">

Instructions:
1.   Log in to your Data Science Virtual Machine with the following command from your local workstation, using CMD or a bash-shell prompt:

`ssh nameyoupicked@ipaddressofyourdsvm`

2. Log in to the system. Now make a directory for the Workshop with the following command:

`mkdir ~/gpu`

3. Change to that directory with the following command:

`cd ~/gpu`

4. Clone the repository using git commands:

`git clone https://msdata.visualstudio.com/DefaultCollection/AlgorithmsAndDataScience/_git/LearnAI-IaaSPaaSforAI`


#### Lab verification
<p><img style="float: left; margin: 0px 15px 15px 0px;" src="./assets/checkbox.png">Enter the following commands to ensure you have several Notebook files:</p> 

`cd ~/gpu/notebooks`

`ls *.ipynb`

<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.5 - Start the Jupyter Notebook Server and Open the Workshop Notebooks

1. You're now ready to continue on to the introduction Jupyter Notebook. Connect to it on your local brwoser using the following URL, replacing the IP Address with the IP Address (or DNS name) of your Linux DSVM, which you can find in the Azure Portal: 

`https://192.168.0.1:8000`

You may get a security warning, since your DSVM is not set up with a signed certificate, but as long as you verify you are connecting to your DSVM's address, you may continue to your site. 

**NOTE: Continuing to a system that is not yours by bypassing the browser's security warning is highly dangerous, and you should exit that screen immediately if the IP address is not correct. Carefully verify that you are accessing the correct site!**

2. If prompted, Click the `Start My Server` button.
3. If prompted, log in with the name and password you set for your Linux DSVM
3. Navigate to the `gpu/notebooks/TODO:` folder and open the `0 - Introduction.ipynb` Jupyter Notebook. Continue the workshop from there. 
