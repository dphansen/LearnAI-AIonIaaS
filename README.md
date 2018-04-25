![](notebooks/assets/solutions-microsoft-logo-small.png)
<img src="notebooks/assets/ai.jpg" style="height:200px;float:right;vertical-align:text-top">

**Course Design Notes - remove after course Charlie-Lock:**

  -  Useful
  -  High Production Value
  -  Deep Learning with GPU (*Package dependency for TensorFlow?*)
  -  Scale-out (*Batch AI*)
  -  Use IaaS DSVM for everything except Model Management/Scale Out
  -  Deploy to IoT
  -  Supporting material can be found here: https://gallery.azure.ai/Collection/Predictive-Maintenance-Template-3 
  
**TODO:**
  - Convert lab notebooks to these notebooks *(complete)*
  - Change readme.md file to have the pre-reqs *(complete, now testing)*
  - Convert experiment to Linux DSVM *(In Process)*
  - Convert tensorflow code to GPU-enabled
  - Include IoT as target (*Process Discovered*)
  - Deploy and test
  - Edit/check pre-reqs and setup - attribute the original *(complete, pending check, reworking as new items discovered)*
  - If the "Answer Key" is needed, make it, if not, remove reference in the first notebook. (*Will not be needed*)
  - Clean up files and directories for consistency, layout, person, and tense

## Artificial Intelligence on IaaS++

#### From the Microsoft Cloud and AI Team

This workshop leads you through a series of [Jupyter Notebooks](https://jupyter-notebook-beginner-guide.readthedocs.io/en/latest/what_is_jupyter.html) that explain how to use the Microsoft Azure Data Science Virtual Machine (DSVM) and the Team Data Science Process (TDSP) to create Data Science and AI solutions. These solutions can be deployed in a variety of ways, leveraging Infrastructure-as-a-Service (IaaS) through Platform-as-a-Service (PaaS) environments, and a mixture of both based on requirements. 

The material for this workshop is intended for a Data Scientist familiar with Machine Learning, Python programming, Artificial Intelligence application development, and a professional backgound in team software development with methodologies such as Agile. [If any of these topics are new to you, we have a learning path here that you can follow to bring you up to speed before you start this workshop](https://github.com/Azure/learnAnalytics-CreatingSolutionswiththeTeamDataScienceProcess/blob/master/Instructions/Learning%20Path%20-%20Creating%20Solutions%20with%20the%20Team%20Data%20Science%20Process.md).

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

### Lab 0.2 - Log in to the DSVM, Explore and Update the System

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">

Whenever you install a new system, it's a good idea to check the environment to ascertain it's configuration. In Linux, the following commands are useful:

Instructions:
1. On your local system, open CMD on Windows or a Terminal Window on Linux. 
2. Type the following commands:
`ssh <Login Name You Created>@<IP Address of your DSVM>`

First, start with the release information of the Operating System:

`lsb_release -a`

Next, examine the hardware: 

`hwinfo -short`

And let's check the drive space:

`df -H`

We notice that the home mount point (/data) doesn't have a lot of room. We'll fix that in a bit.

Finally, let's update the system:

`sudo apt-get update`

*(You may be prompted for the password you set in the Portal when you created the VM)*

`sudo apt-get upgrade`

#### Lab verification
<p><img style="float: left; margin: 0px 15px 15px 0px;" src="./assets/checkbox.png">Commands complete successfully.</p> 
 
<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.3 - Clone the Workshop's Jupyter Notebooks

<img src="notebooks/assets/checkmark.jpg" style="float:right;vertical-align:text-top">


Instructions:
1. We'll need more space for the labs, since /data doesn't have enough to do what we need to do. Log in to the DSVM, and clone the course with the following command:

`sudo mkdir /gpuclass`

2. Then grant access to it for everyone (in production, you would limit the access to only certain groups, and determine for each file whether they need read/write/execute):

`sudo chmod -R 0777 /gpuclass`

3. Now clone the course with the following command:

`git clone -b bwoody-coursealpha https://msdata.visualstudio.com/DefaultCollection/AlgorithmsAndDataScience/_git/LearnAI-IaaSPaaSforAI /gpuclass`

4. And link to it with the following command:

`ln -s ~/notebooks/gpuclass /gpuclass`

We should now be able to see the course materials when we access the notebook server. 

#### Lab verification
<p><img style="float: left; margin: 0px 15px 15px 0px;" src="./assets/checkbox.png">Enter the following commands to ensure you have several Notebook files:</p> 

`cd ~/notebooks/LearnAI-IaaSPaaSforAI/notebooks`

`ls *.ipynb`

<p style="border-bottom: 3px solid lightgrey;"></p>

### Lab 0.4 - Start the Jupyter Notebook Server and Open the Workshop Notebooks

1. You're now ready to continue on to the introduction Jupyter Notebook. Connect to it on your local brwoser using the following URL, replacing the IP Address with the IP Address (or DNS name) of your Linux DSVM, which you can find in the Azure Portal: 

`https://<IP Address of your DSVM>:8000`

You may get a security warning, since your DSVM is not set up with a signed certificate, but as long as you verify you are connecting to your DSVM's address, you may continue to your site. 

**NOTE: Continuing to a system that is not yours by bypassing the browser's security warning is highly dangerous, and you should exit that screen immediately if the IP address is not correct. Carefully verify that you are accessing the correct site!**

2. If prompted, log in with the name and password you set for your Linux DSVM
3. If prompted, click the `Start My Server` button.
4. Navigate to the `~/notebooks/LearnAI-IaaSPaaSforAI/notebooks` folder and open the `0 - Introduction.ipynb` Jupyter Notebook. Continue the workshop from there. 
