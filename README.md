# Welcome

Welcome to this one day workshop on using Azure IaaS and PaaS for AI workloads. 
In these two days, we will focus on hands-on activities that develop proficiency in AI-oriented workflows leveraging 
the Data Science Virtual Machine and other Azure offerings. 
These labs assume a introductory to intermediate knowledge of these services, and if this is not the case, then you should spend the 
time working through the pre-requisites.

## Pre-requisites

Pre-requisites can be found [here][prereq3.0]. Briefly, pre-requisites include the following:

### Resources

- The ability to create resources within an Azure subscription
- Familiarity with how to create resources in said subscription

### Languages

- Python

## Goals (keeping just to note format)

- Understand and use the Team Data Science Process (TDSP) to clearly define business goals and success criteria
- Use a code-repository system with the Azure Machine Learning Workbench using the TDSP structure
- Create an example environment
- Use the TDSP and AMLS for data acquisition and understanding
- Use the TDSP and AMLS for creating an experiment with a model and evaluation of models
- Use the TDSP and AMLS for deployment
- Use the TDSP and AMLS for project close-out and customer acceptance
- Execute Data preparation workflows and train your models on remote Data Science Virtual Machines (with or without GPUs) and HDInsight Clusters running Spark
- Manage and compare models with Azure Machine Learning
- Explore hyper-parameters on Spark using Azure Machine Learning
- Deploy and Consume a scoring service on Azure Container Service
- Collect and Analyze data from a scoring service in production to progress the data science lifecycle.

# Agenda

Please note: This is a rough agenda, and the schedule is subject to change pending class activities and interaction.

1.	Data Acquisition and exploration:
  a.	Accessing data from different data sources (like Blobs, Azure File Shares, SQL DB/DW, CosmosDB, Spark, Data Lake, to/from local machine) from the DSVM
  b.	Data exploration and pre-processing using Python, PySpark, R
2.	Modeling:
  a.	Building Deep learning models locally on the GPU instances of DSVM, scaling out training on BatchAI
  b.	Building Spark MLLib/MMLSpark locally for development, scaling out on aztk (and possibly Databricks that is the focus going forward compared to HDI). 
3.	Deploying models:
  a.	AzureML Container/Kubernetes  based deployment (Realtime now, Batch coming soon) – Maybe a pointer to existing AzureML material 
  b.	Deploying DL/Spark models for batch scoring on aztk/BatchAI/Databricks
  c.	Deploying models on Tensorflow Serving
  d.	Other ways to deploy models – Natively on DSVM (for small data) using Flask etc, Azure Functions, App Services
  e.	Future ONNX Model export and deployment (TBD)
4.	Enterprise features: (We recently worked on this in the DSVM team and planning to some documentation/scripts in a couple of weeks)
  a.	Single Signon with Active Directory domain join
  b.	VM Scale Sets for scaling team’s DSVM Pool 
  c.	Using Managed Service identity (MSI) for access to resources without embedding credentials
  d.	Security : Controlling access to data sets


# Discussion Forum

Include?

# Software Dependencies

These materials have been tested on Windows with:

- DSVM version?
- AML deployment version? if using?

[prereq3.0]: https://aka.ms/learnai-proaidevbootcamp-03-0
[lab3.1]: https://aka.ms/learnai-proaidevbootcamp-03-1
[lab3.2]: https://aka.ms/learnai-proaidevbootcamp-03-2
[lab3.3]: https://aka.ms/learnai-proaidevbootcamp-03-3
[lab3.4]: https://aka.ms/learnai-proaidevbootcamp-03-4
[lab3.5]: lab03.5-execute_remote_gpu/0_README.md
[lab4.1]: https://aka.ms/learnai-proaidevbootcamp-04-1
[lab4.2]: https://aka.ms/learnai-proaidevbootcamp-04-2
[lab4.3]: https://aka.ms/learnai-proaidevbootcamp-04-3
[lab4.4]: https://aka.ms/learnai-proaidevbootcamp-04-4
[lab4.5]: https://aka.ms/learnai-proaidevbootcamp-04-5
[gitter]: https://gitter.im/LearnAI-Bootcamps
