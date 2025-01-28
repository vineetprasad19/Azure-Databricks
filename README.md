# Azure-Databricks
Azure Databricks is an Apache Spark-based analytics platform optimized for the Microsoft Azure cloud. It is a collaborative, cloud-based environment designed for data engineering, machine learning, and analytics workloads. Azure Databricks integrates seamlessly with Azure services like Azure Data Lake Storage, Azure SQL Database, Azure Machine Learning, and Power BI, making it a powerful tool for modern data processing and analytics.  

# What is Azure Databricks Used For? 
**Data Engineering:**  
Ingesting, cleaning, and transforming large datasets for further analysis.  
ETL (Extract, Transform, Load) processes at scale.  
Real-time and batch processing of data.  
**Data Science & Machine Learning:**  
Experimentation with machine learning models using distributed computing.  
Training large-scale machine learning models.  
Deploying models for real-time or batch inference.  
**Big Data Analytics:**  
Processing large-scale structured and unstructured datasets.  
Running SQL queries on massive datasets using Spark SQL.  
Creating interactive dashboards and visualizations.  
**Business Intelligence:**  
Enabling advanced analytics for decision-making.  
Integrating with Power BI for visualization of processed data.  
**Streaming Analytics:**  
Handling real-time data streams from IoT devices or event hubs.  
Building real-time analytics pipelines.  

**Steps**  
Create Azure Account  
Create Resouce group  
Create Work Space  

![image](https://github.com/user-attachments/assets/2e2440ab-0a85-47e8-a9e4-5a76e1a40fc2)

Once the Resource is created, pin it to the dashboard. 
![image](https://github.com/user-attachments/assets/369ec083-de3f-4bbb-b4d4-d92b94d0da2a)

Go back in the dashbaord and databricks and launch it.
![image](https://github.com/user-attachments/assets/f421c3a7-3f91-427c-889c-e2156477308d)

**Azure Databricks Architecture**  
![image](https://github.com/user-attachments/assets/1a03dfc7-68ec-455e-886a-f11709f78e9b)

![image](https://github.com/user-attachments/assets/a6b6db04-8649-4d89-8b21-cf2eb3fd5249)

# Databricks Clusters  
1. What is databricks cluster  
2. Cluster types  
3. cluster configuration  
4. creating a cluster
5. cluster pools
6. cluster policy

**1 What is databricks cluster**  
It is a distributed computing system designed to efficiently process large-scale data. Databricks clusters are highly configurable and can automatically scale to accommodate workload requirements.  

Key Components of a Databricks Cluster:  
**Driver Node:**  
Orchestrates the execution of tasks and manages the distribution of work across worker nodes.  
Responsible for managing the cluster state and communicating with the Databricks control plane.  
**Worker Nodes:**  
Perform the actual computation and data processing tasks.  
Each worker node has a set of executors that execute the tasks assigned by the driver node.  
**Cluster Manager:**  
Allocates resources across the nodes and monitors cluster health.  
Ensures that tasks are scheduled efficiently.  
**Databricks Runtime:**  
Includes Apache Spark and additional libraries optimized for Databricks.  
Pre-configured to support common data science and engineering workflows.  

![image](https://github.com/user-attachments/assets/8f198209-1d10-4f39-80a6-9c83b23b1d3b)

**2 Cluster Types**  
![image](https://github.com/user-attachments/assets/413b2984-4bfc-4a05-a085-73dab87d079f)

**3 cluster configuration**  
First, we have the option to choose whether we want to create a **Single Node** or a **Multi Node Cluster**.  
**Multi Node Cluster** will have one Driver Node and one or more Worker Nodes.  
When you run a Spark Job against a Multi Node Cluster, the Driver Node will distribute the tasks to run on the Worker Nodes in parallel, and returns the result.  
They give us the ability to horizontally scale the Cluster depending on your workload.We can basically keep adding Worker Nodes as we need.  
These are the default type of Clusters used for Spark Jobs and suitable for large workloads.  

On the other hand, S**ingle Node Cluster** will have only one node, which is the Driver Node and there are no Worker Nodes.  
Even though, there are no Worker Nodes, Single Node Clusters also supports Spark workloads.  
When you run a Spark Job, the Driver Node acts as both the driver and the worker. As there are no Worker node, the Single Node Clusters are not horizontally scalable, so they're not suitable for large ETL workloads. They're mainly targeted for lightweight Machine Learning and Data Analysis workloads which don't require, any distributed compute capacity.

We then need to define the **Access Mode.**  
There are **3 different types of Access Modes** available at the moment for the Cluster.  
As the name suggests, **Single User access** mode only allows a single user to access the Cluster. **It supports all four languages Python, SQL, Scala, and R**.  
**Shared access mode** allows the Cluster to be shared amongst more than one user, but it provides process isolation. Each process gets its environment, so one process can't see the data or the credential used by the other one.  
It's only available on premium workspaces. Also, **it only supports Python and SQL workloads.**  
**No Isolation Shared** also allows the Cluster to be shared amongst more than one user. It's available on both standard and premium workspaces. Also, **it supports all four languages Python, Scala, SQL and R.**  
The main difference between this and the Shard access mode is that, No Isolation Shared access mode doesn't provide any process isolation. So failure in one user's process may affect the others. Also, they don't offer any task preemption, so one running process may use all the resources and the others may fail.

And most importantly, as everything is shared, it's considered less secure. **Custom access mode** is not an option, when you create the Cluster using the latest user interface. You're only likely to see this if you have already created a Cluster using the **legacy configurations.** 

![image](https://github.com/user-attachments/assets/78c712b3-c00c-422c-9472-dc8fdce7fb27)

**Databricks runtimes**  
Databricks runtimes are the set of core libraries that run on Databricks Clusters.  
**Databricks Runtime, Databricks Runtime ML, Photon Runtime and Databricks Runtime Light.**  

Databricks Runtime includes an optimized version of Apache Spark Library. Java, Scala, Python and R Libraries, Ubuntu and its accompanying system Libraries, GPU Libraries for GPU enabled Clusters, Delta Lake Libraries and also other Libraries for Databricks services  that integrate with other components of the platform such as **Notebooks, Jobs and Cluster Manager.**  

**Databricks Runtime ML** includes all the libraries from the Databricks Runtime, plus the popular ML Libraries such as PyTorch, Keras, TensorFlow, XGBoost, etc..  

**Photon Runtime** also includes all the libraries from the Databricks runtime, plus the Photon Engine, which is the Databricks native vectorized query engine, that runs SQL workloads faster and reduces your cost per workload.  

**Databricks Runtime Light** is the runtime option for only jobs not requiring advanced features such as auto scaling, reliability and improved performance. Also, it's only suitable for Automated Workloads.  
You can't use it for Interactive Workloads or Notebook Jobs.  
Auto Termination is a nice feature that will avoid unnecessary costs on idle Clusters.  
It's especially useful on Ad-hoc clusters for preventing them, running during evenings and weekends when they're not in use.  
You can specify when to terminate your Databricks Cluster, if the cluster has not been in use. It will be terminated after the number of minutes specified.  

![image](https://github.com/user-attachments/assets/d982e44e-bc8c-4cd2-9299-cd51f98d8568)

Default value for **Auto Termination is 120 minutes**, but you can change the value.  
The accepted values range from 10 to 10000 minutes.  
When you create a Multi Node Cluster, you can specify the minimum and the maximum number of Worker Nodes.  
**Auto Scaling** will automatically add or remove nodes from the Cluster depending on your workload. This can result in optimum utilization of the Cluster.  
This is especially useful if you're unsure about the workload upfront or your workload changes throughout the process.  
They're not recommended for streaming workloads, even if specified Databricks defaults to the maximum number of Worker Nodes.  
There are a wide array of **Azure VM types** available for us to use.  
Databricks groups them into small number of easy to understand groups.  
**Memory Optimized instance types** are recommended for memory intensive applications. For example, a Machine Learning workload that caches a lot of data in memory.  
**Compute Optimized instance types** can be useful for structured streaming applications, where you need to make sure that the processing rate is above the input rate at peak times of the day.  
These can also be used for Distributed Analytics and Data Science Applications.  
**Storage Optimized instance types** are recommended for use cases requiring high disk throughput and I/O.  
**General Purpose instance types are** are recommended for Enterprise Grade applications and analytics with In-memory caching.  
**GPU Accelerated instance types** are recommended for Deep Learning Models, that are data and compute intensive.  
**Cluster Policy Configuration** This could easily overwhelm a Data Engineer or a Machine Learning Engineer, and creating Clusters become the sole responsibility of the administrator. Because it's too difficult to configure for a Standard Data Engineer or a Machine Learning Engineer. Also, without careful consideration, users could accidentally create Clusters which are oversized and too expensive to run. Cluster Policies help us avoid these common issues. Administrators can create Cluster policies with restrictions, and assign them to users or groups. When a Cluster Policy is selected, the configuration becomes much more simplified. In summary, Cluster policies simplify the user interface, thus enabling standard users to create Clusters and take away the need for administrators to be involved in every decision. And most importantly, it achieves cost control by limiting the maximum size of the Clusters. But please note that this is only available on premium tier.  

Hope you now have a good understanding about the **configurations** you can specify for a Cluster.  

**4 Creating Databricks Cluster**  

![image](https://github.com/user-attachments/assets/7724b84a-e4e6-4236-a2ab-5a316527ae73)

![image](https://github.com/user-attachments/assets/ed38e93a-607d-475f-9b72-39050d569ef1)

![image](https://github.com/user-attachments/assets/81a49047-66bc-456f-a6b8-90046ac44b4e)

**5 Cluster Pools**  
A Cluster Pool is basically a set of idle ready to use virtual machines, that allow us to reduce the Cluster start and Auto Scaling times.  
For example, let's assume that we have created a Pool with a minimum of 1 idle instance and 2 maximum instances. What this means, is the pool will always keep at least one instance ready for Clusters to consume until, it reaches the maximum limit, which is two in this case. Let's say Cluster 1 comes along and requests for one node. Pool gives the one instance to the Cluster and spins up another one ready.  
If Cluster 2 requests for one more node, then it gives that one to the Cluster 2. But instead, if Cluster 2 requests for two more, it will fail to start with error that there are enough instances available to allocate.  

![image](https://github.com/user-attachments/assets/1929ea4c-423b-4de9-b843-9512645db4bb)

![image](https://github.com/user-attachments/assets/3a87b8fe-c7f1-4f60-bb74-d9ef8d24aced)

**6 Cluster Policy**  
Creating the wrong type of Cluster could increase the cost of running the project and also can affect data security. So if we expect standard users to create the Cluster and keep the cost down, we should simplify the interface and make it easier for them.
That's where Cluster Policies come in. Policies are basically a set of rules which allows us to hide or take out the configuration options, that are not required on the user interface. They allow us to fix the values of some of the configuration parameters and restrict access for the users so that they're not changing them. Also, in a set of values, a policy allows us to select default values on the user interface.
An administrator can create a policy and assign that to a set of users. When the user chooses the policy, they'll now have a Simpler User Interface because some of the options are now hidden or pre-populated with fixed values. Only allowing the users to select certain type of nodes or setting Auto Termination by Default, allows us to keep the cost down.
It helps us having standard type of Clusters created by all users in a specific group. And finally, cluster policies take away the need for an administrator to be involved in every cluster creation decision and empowers standard users to create them.

![image](https://github.com/user-attachments/assets/4f63ae81-449e-4f05-82d6-fa11639518c9)

![image](https://github.com/user-attachments/assets/c95eea7d-b6b9-43e5-ac37-42f2d86d3a00)

![image](https://github.com/user-attachments/assets/ec114ff6-70d1-4fba-80b5-7f334f6ba5fd)

# Databricks Notebooks  

We are going to see below things, 
1. What's a notebooks  
2. Creating a notebook  
3. Magic commands  
4. Databricks utilities  

**1. What's a notebooks**  
A notebook is a collection of cells, that run commands on a Databricks Cluster.  

**2. Creating a notebook**  

![image](https://github.com/user-attachments/assets/3b692fd5-bfe9-4ba2-937b-848a440f699d)

**You can Export in**  
![image](https://github.com/user-attachments/assets/0be68078-3e2f-42d9-af65-fd3d97c170f9)

**Notebook formats**  

You can export the notebook in any of these four format specified here. If you're not familiar with the DBC file format, that's the Databricks Binary File format, which allows us to export not only individual notebooks, you can also export the entire folder and also it can contain any types of files in it. And you can then import that DBC file into another Databricks workspace or within the same Databricks workspace into another folder later. So that's really really useful, if you're working with Databricks. If you choose the Source file format, each notebook will be exported as separate files in Source file format.  
For example, . py for this notebook, as it's a Python Notebook.  
If you had a SQL notebook, you will have a file with the extension of .SQL.  
IPython will export the file in IPython format. By default notbooks are in Python format.  
Finally, HTML will export as a single HTML file for each of the notebook. Edit menu gives you the standard edit options such as cut, copy, paste and things like that.  
And also, if you're working with Python, you have the option here to set your indentation to be two spaces or four spaces depending on your preference. And View, lets you view your notebook in different ways.  
![image](https://github.com/user-attachments/assets/f60fcd9e-7aa9-43eb-97bb-296b088353f3)

**Notebooks Keyboard Shortcuts**  
![image](https://github.com/user-attachments/assets/0290e01d-e15d-4100-98a0-8e3a94a2b3dd)

**3. Magic commands**  
The primary purpose of the Magic Commands, is to override the default language in a Notebook. For example, you may want to switch from Python to Scala within the same notebook. There are also some auxiliary magic commands which allow us to create documentation in our notebooks and access the file system, etc..  

As we know, the default language for this notebook is Python. And let's say I want to run a SQL statement, so let me try that. And as you can see here, we've got an error saying invalid syntax.  
That's because, Python doesn't know how to execute a SQL statement. So we need to execute this as a SQL statement. So in order to do that, Databricks offers something called a Magic Command.  
So you just have to specify a **%SQL** and then run the Select statement. Now, the context of this cell alone has changed from **Python to SQL**.  
However now if you just write **Select * ,the notebook** automatically recognize that this is SQL language and it changes the notebook **language to SQL**.  

![image](https://github.com/user-attachments/assets/6e182794-0798-4bc5-b96d-f4576c667142)

Similarly, if you wanted to run a Scala statement, you would use the magic command **%Scala**  
Apart from being able to switch between these four languages, Databricks also offers few auxiliary magic commands, which are quite handy.  
**%md** So this gives you the ability to document your notebook quite nicely and make it usable for everyone, particularly someone not familiar with this notebook. You can also embed HTML images, etc., which is really good.  

**file system magic command, which is percentage %fs.**  
![image](https://github.com/user-attachments/assets/98f92c64-5ee4-40e3-a74c-b34345b15115)

**Finally, the last magic command I want to talk you through is the Shell command %sh.**  
Let's say we want to see all the processes that are running. I can just use the ps command to do that. And that's showing us all the processes that are running in this Cluster.  
![image](https://github.com/user-attachments/assets/fd577964-b872-478f-b213-28dee4ddc1e4)

**4. Databricks utilities**  
Databricks Utilities make it easier to combine different types of tasks in a Single notebook. For example, they allow us to combine file operations with ETL tasks.
These utilities can only be run from Python, Scala or R cells in a Notebook. They cannot be run from a SQL cell.
Databricks have been coming up with a number of utilities recently. Some are in preview and others are available for general availability. Amongst those, the following are the most commonly used utilities.
Secrets Utilities allow us to get secret values from secrets, which are stored in secret scopes backed by Databricks or Azure Key Vault. Widget Utilities allows us to parameterized notebooks so that a calling notebook or another application, for example, a Data Factory Pipeline can pass a parameter value to the notebook at runtime. This is really useful to make a notebook reusable. Notebook Workflow Utilities allow us to invoke one notebook from another and chain them together.

![image](https://github.com/user-attachments/assets/ecceb684-4e79-41f1-bd16-b19314011c74)

![image](https://github.com/user-attachments/assets/7264a2b8-3706-4c4d-ad26-7f8f01b8bd89)

If you ask me when to use the %fs command and when to use the dbutils package, I tend to use %fs magic command if I'm doing some ad-hoc queries, and I use the dbutils.fs package if I'm doing something programmatically like this. So far we've only been working with Python, but you can do the same with Scala and R, but you can't do this with SQL.  

![image](https://github.com/user-attachments/assets/242f5026-d6dd-4682-86f9-5025619d7030)

![image](https://github.com/user-attachments/assets/2781a389-5969-4972-80a3-5106777b3db6)

# Azure Data Lake (ADLS)

![image](https://github.com/user-attachments/assets/830af93d-99af-435f-9c3d-f6e4a84c57de)

Each Azure Storage account comes with an access key that we can use to access the storage account. Also, we can generate a special kind of key called shared access signature or otherwise referred to as SAS token, and we can use that to access the storage account. SAS tokens lets us manage access at a more granular level than the access key. We can also create a service principal and give the required access for the data lake to the service principal, and use those credentials to access the storage account.
All of these three options can take two forms.  
The first one is to use these credentials in the notebook and authenticate to the data lake. The authentication in this scenario will be valid just for the duration of the session, i.e. until the notebook has been detached to the cluster. This is called session scoped authentication.  
The other option is to use these credentials in the cluster and authenticate from the cluster. The authentication will happen when the cluster starts, and it will be valid until the cluster has been terminated. All the notebooks connected to this cluster will have access to the data. This is called cluster scoped authentication.  
Apart from these, there are two more forms of authentication patterns available in Databricks.  
First one is called the AAD Pass through authentication or otherwise referred to as the Azure Active Directory pass through authentication. In this pattern, we just need to enable the cluster to use Azure Active Directory. Pass through authentication. Whenever a user runs a notebook, the cluster will use the user's Azure Active Directory credentials and look for the roles the user has been assigned to the Azure Data Lake Storage using IAM or Identity and Access Management. If the user has access to the storage account, it will allow the user to access the storage account. Otherwise, the user won't be able to access the storage. AAD pass through authentication is only available on premium workspaces.  
The last one is the most recent addition to Databricks, called Unity Catalog. In this access pattern, the administrators can define the access permissions for a user using the Databricks Unity Catalog. When a user is trying to access the storage account, the cluster will check for the user's access in the unity catalog. If the user has the required permissions, it will allow the user to access the storage account, otherwise they won't be able to access.  

**First Lets create a Azure Storage Account.**  

![image](https://github.com/user-attachments/assets/e0ba0b80-b93e-48f3-8b73-0779d954a484)

![image](https://github.com/user-attachments/assets/50299e56-0814-4ecc-bf1e-9840232e9e7c)

![image](https://github.com/user-attachments/assets/bc10e86a-9dab-4b19-88f5-b850840cdb3d)

![image](https://github.com/user-attachments/assets/faa56980-f3d7-44d5-9be4-ab9b2ff10d5e)

![image](https://github.com/user-attachments/assets/394d0555-c0c4-4589-94a5-2cf113f06841)

![image](https://github.com/user-attachments/assets/af199b7e-ba89-4e96-b9f9-cbf6bda6dfd1)

**Lets Create Containers now**  
Containers are just to hold your files, grouped together into one place.  

![image](https://github.com/user-attachments/assets/a770df96-3544-4659-ab48-443a40eed19c)

![image](https://github.com/user-attachments/assets/8ea53525-c832-48a0-8f17-fee5308868c4)

Upload a file in the container you just created.  

![image](https://github.com/user-attachments/assets/40e7867c-6326-4fb0-9aa2-e558c0b12ae9)

So click on the file name and you can click on Edit, for example, to edit the data and you can click on Preview to preview the data. So I uploaded a csv file, so I've got these columns and it's nicely formatted the data And also you've got the option to come and delete the file from here for example, and you can Rename the file, you can do everything that's stated here. And also, if you wanted to create a new folder within our demo container, you can simply click on Add Directory and then create the folders. You can have any number of nested folders within the container as well. it's very similar to working with any other file system storage, such as in Windows or in Linux, But there are some limitations with this web user interface.

# Azure Storage Explorer
this web UI doesn't allow us to upload folders. We can only upload individual files, and also you can't see all your storage accounts in your subscription in one place. You need to navigate to each of the storage accounts to see the files and folders in it. Azure Storage Explorer desktop version makes all of it a lot easier and offers many more features. In order to download the Azure Storage Explorer, go to the Storage browser here on the left hand side menu, and click on Download Azure Storage Explorer, that opens up the downloads page for **Storage Explorer**. You can also search using Google or Bing to find the URL  https://azure.microsoft.com/en-us/products/storage/storage-explorer/#Download-4  
Select your computer's operating system and that downloads the software for you and you just need to install it in your Laptop or Computer.  

![image](https://github.com/user-attachments/assets/a64d1c9c-48a1-4756-97e5-02f3a62ce2cc)

![image](https://github.com/user-attachments/assets/754a5893-ec5f-48de-a6a9-22319ab81769)

**Installed successfully.**

![image](https://github.com/user-attachments/assets/8d10d045-5ce8-4d76-b0da-60bcf7d642bd)

**All these things you can do with Azure Storage Explorer.**

![image](https://github.com/user-attachments/assets/13149be6-2f77-4d33-acf7-2552fff86a49)

As you can see, it's a handy tool to have in your workstation when you're working on a production environment.

**Access Key Authentication**
![image](https://github.com/user-attachments/assets/71ab149b-141b-4118-b43b-122d6956946b)

**Access keys - Spark Configuration**
![image](https://github.com/user-attachments/assets/b6a1804e-5d1a-4a04-9af4-26c2d2bc1b43)

The configuration parameter has two parts. The first part is the config fs.azure.account.key, followed by the endpoint of the storage account. In this case, that's Storagename.dfs.co.windows.net. We then provide the 512 bit access key for the storage account as the second parameter. Using this Spark configuration, Databricks will now be able to authenticate to the storage account.

**Access keys - Azure Blob File System Driver**
![image](https://github.com/user-attachments/assets/92834c7e-1a6a-4d7c-b24e-1d60a7d7dfe7)

Now without access keys i was trying to connect to my **Azure storage Account from Databricks** and it failed as I don't have access keys. 

![image](https://github.com/user-attachments/assets/29e73624-a9e6-4ed1-bf15-cd6458c27a1c)

Go back to the storage Account, click Access keys and copy the access key. 

![image](https://github.com/user-attachments/assets/fb8c1b77-b051-429d-8043-d47e22743861)

Now connect the storage account container from datarbicks using Spark. 
**Note:** Make sure you disable blob soft delete option, I figured out that it was not connecting with the access key when it was enabled.

![image](https://github.com/user-attachments/assets/400e41d5-9a20-4a5d-8aec-af96fe10d3d1)

So in above step we configured access keys with spark config command, list files using python, and read data from flatfile using spark.

**Shared Access Signature**
![image](https://github.com/user-attachments/assets/0de22bb7-aa06-4457-b107-630edf052a35)

![image](https://github.com/user-attachments/assets/0353d772-b0b5-469a-9625-cd0cfec461e4)

**Shared Access Signature (SAS) Token**
A shared access signature (SAS) is a URI that grants restricted access to an Azure Storage container. Use it when you want to grant access to storage account resources for a specific time range without sharing your storage account key.

Url: https://learn.microsoft.com/en-us/azure/databricks/connect/storage/azure-storage#access-azure-data-lake-storage-gen2-or-blob-storage-using-a-sas-token
spark.conf.set("fs.azure.account.auth.type.<storage-account>.dfs.core.windows.net", "SAS")
spark.conf.set("fs.azure.sas.token.provider.type.<storage-account>.dfs.core.windows.net", "org.apache.hadoop.fs.azurebfs.sas.FixedSASTokenProvider")
spark.conf.set("fs.azure.sas.fixed.token.<storage-account>.dfs.core.windows.net", dbutils.secrets.get(scope="<scope>", key="<sas-token-key>"))

**Generate SAS Token for specific container.**

![image](https://github.com/user-attachments/assets/d04badeb-b36e-48d8-8c78-527c84816376)

![image](https://github.com/user-attachments/assets/8b438f1f-1242-4e61-bad6-9c40703e5f61)

![image](https://github.com/user-attachments/assets/40550370-f775-45ce-a2b0-f08dee916b26)

![image](https://github.com/user-attachments/assets/895ef366-75db-44a4-9a42-9bf89bdb8a32)

# Service Principal  
we are going to look at accessing the Data Lake Storage using **Azure Service Principal**. Service Principals are quite similar to user accounts. They can be registered in the Azure Active Directory and assigned permissions required to access the resources in the Azure subscription via role-based access control or RBAC.  
Azure makes a number of standard roles available, and you can also create custom roles.  
**Service Principals** are the recommended method to be used in automated tools such as **Databricks jobs** as well as in CI/CD pipelines. This is because they provide better security and traceability.  
In a good architecture, each Application will have its own Service Principal, and the **Service Principal is just assigned the required permissions on the resources.** All of this can be audited and monitored. So this provides better security and monitoring. As you can see, using a Service Principal to access the Data Lake is slightly more involved than the other options we've seen so far.   
**Steps**  
1. we need to register the Service Principal. Service Principal is also referred to as Azure AD Application or Active Directory Application. Each Application that's registered is given a unique identifier called an Application or a client ID.  
2. create a secret for the Service Principal.   
3. configure Databricks to access the storage account via the Service Principal. We can do that by setting some Spark configuration parameters.  
4. We then need to assign the required role on the Data Lake for the Service Principal so that the Service Principal can access the data in the Data Lake. The Role, Storage Blob Data Contributor, gives full access to the storage account, But you can also use Storage Blob Data Reader if your Application only needs a read-only access.  

![image](https://github.com/user-attachments/assets/67c3ab56-e5cd-4f85-8f64-c719436e60a8)

To Register, go to Azure Active Directory and Click App Registration  
![image](https://github.com/user-attachments/assets/d1ae39dd-10e3-459f-aecf-feef3fc8d54f)

![image](https://github.com/user-attachments/assets/af5fc480-7645-42a0-9d2f-9eb98380f512)

Now create secret keys. 
![image](https://github.com/user-attachments/assets/b874c129-0319-4779-a71d-cd6e362dcedd)

spark.conf.set("fs.azure.account.auth.type.formula1dlrack.dfs.core.windows.net", "OAuth")  
spark.conf.set("fs.azure.account.oauth.provider.type.formula1dlrack.dfs.core.windows.net", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")  
spark.conf.set("fs.azure.account.oauth2.client.id.formula1dlrack.dfs.core.windows.net", client_id)  
spark.conf.set("fs.azure.account.oauth2.client.secret.formula1dlrack.dfs.core.windows.net", client_secret)  
spark.conf.set("fs.azure.account.oauth2.client.endpoint.formula1dlrack.dfs.core.windows.net", f"https://login.microsoftonline.com/{tenant_id}/oauth2/token")  

Now Add a Role assignment to your storage Account  
![image](https://github.com/user-attachments/assets/e5a019af-7b34-4ab2-91a8-0093e170002a)

Add App/member to the role. 
![image](https://github.com/user-attachments/assets/0823b63b-7c2f-40eb-a8f8-5279ebb941f0)

![image](https://github.com/user-attachments/assets/68a6a465-03cb-40f0-813c-88307551df07)

So all we've done here is that we've given the Storage Blob Data Contributor access on our storage account to the Service Principal. So the Service Principal can now access the storage account.  

Now go back to your notebook and runall. 

![image](https://github.com/user-attachments/assets/58785080-56f7-4f62-8a17-1127bc2fc425)

As you can see here, we have successfully managed to access our storage account. So we've got the file being listed here and the data is being read as well. So with that we've successfully managed to use the Service Principal to access our storage account from Databricks.  

Instead of keeping the access keys in notebook and running the spark job, we can configure the access keys in cluster itself so cluster can validate for us when runnning the notebook jobs, but this is not the best practice as some may have different access and we don't want them to access all via cluster authentication.  

The best is the **Active directory credential Passthrough**. We might want to restrict access to users based on what they can see via the Active Directory account. This is what is called AAD or Azure Active Directory credential pass through authentication. Effectively, Databricks will pass the user's Azure Active Directory credentials to the ADLs storage account to authenticate if the specific user has the required role assigned in Rbac for the storage account. They'll be able to access the storage account, otherwise they won't be able to access the storage account. This is really useful in scenarios such as multiple machine learning engineers, or using the same Databricks cluster, but each one should have access to only specific storage accounts. NOw this is called as **Unity Catalog** so look into it.  
![image](https://github.com/user-attachments/assets/51865838-fd00-4e4d-9e4b-38f5b775bf28)

# Unity Catalog
Unity Catalog is a databricks offered unified solution for implementing data governance in the Lakehouse.  
Data Governance is the process of managing the availability, usability, integrity and security of all the data present in an enterprise. An enterprise should be able to control access to the data to only the users who should have the access. Because not having the right access control could compromise the customer data and the reputation of the enterprise. A successful implementation of a data governance solution will ensure that the data is trustworthy and not misused. It requires the ability to trace the data back to its source for authenticity and also the ability to audit the usage of the data to ensure that it is not misused. It must help implement privacy regulations such as GDPR, CCPA, etc. Non-compliance with these regulations could land companies with hefty penalties and bad reputation with the customers. So it's important that companies implement the right data governance solution. These are the general characteristics of a good data governance solution.  


Unity Catalog offers data access control by restricting access to only the required users and groups. In Databricks, this means implementing access control to files stored in the Data Lake. The tables created in Databricks as well as notebooks, dashboards and machine learning models. Once the user is given access, we should be able to see how the user is using the data and how often and when it's being accessed. So we need some audit information of the data access to be logged and made available.  
Unity Catalog makes the necessary audit logs available to do this. We also need to be able to identify the trustworthiness of the data. This means we need to be able to trace back the data to its source to ensure the authenticity.  
Unity Catalog provides lineage of the data both upstream and downstream in a pipeline so that you can visually see the flow of the data and how it's transformed during the journey. It not only helps identify the authenticity of the data, but also gives us the ability to trace back the root cause of any potential issues with the data.  
Finally, if you worked in a Data Lake, you will appreciate the difficulty of being able to identify the right data asset for your project amongst the several thousand data assets in a Data Lake. Databricks makes a searchable data catalog available with the help of Unity Catalog.  
Unity Catalog brings all of these together to implement a unified data governance solution for the data Lakehouse platform.  
![image](https://github.com/user-attachments/assets/a8e99b4f-adc6-4d85-9148-e2ea69e6855c)

![image](https://github.com/user-attachments/assets/bb1a6c5c-b639-4342-8ba9-b72ff8af15a5)

databricks recommends using one metastore per region. The reasons for this recommendation is to reduce the egress cost as well as improve performance. So please create one metastore per region and keep your databricks workspace and the default storage in the same region to get the best performance and reduce cost.  
![image](https://github.com/user-attachments/assets/ef144ead-1742-4af8-b7f9-ec72a9d6f613)

**Unity Catalog Setup**
![image](https://github.com/user-attachments/assets/d874b104-ad2a-4dc8-859f-362434027478)

Create a new workspace.
![image](https://github.com/user-attachments/assets/b2811e5c-3dc8-4f6b-ba16-3aa36a7abfcd)

Create a new storage account as Data Lake Storage Gen2
![image](https://github.com/user-attachments/assets/d935de79-b36c-4d3e-a1e3-a04627dcf262)

Create access Connector for Azure Databricks.
![image](https://github.com/user-attachments/assets/4ecab287-a3d1-443c-9cbd-d7a8b0caefc5)

![image](https://github.com/user-attachments/assets/58b5b829-0700-4117-84bb-d1663fd00d43)

Now last thing we want to do is to **assign the role Storage Blob Data Contributor** on our Data Lake to the access connector we just created.  
![image](https://github.com/user-attachments/assets/aadb0029-37d0-4bc6-912c-9ccbe4c682e9)

![image](https://github.com/user-attachments/assets/71db71bd-a0bd-4f57-a0c4-e9de8e268e32)

Firstly, all managed tables in Unity Catalog are Delta tables. You cannot create a table with format Parquet, JSON, CSV, etc., as Managed Tables. For that you will have to use External Tables. Second, by default, the data for Managed Tables will be written to the default storage used to configure the metastore. If you remember, it used to be the DBFS root in Hive Metastore, but now it's the storage account we attached to the metastore while creation. You can change this to a different location by specifying a managed location in your create schema or create catalog statements. In Hive Metastore when you drop a managed table, the underlying data is deleted immediately. But in Unity Catalog enabled workspace, the data will be retained for 30 days. This is a great addition which a lot of people were requesting for. It takes away the fear of accidentally losing the data. Managed tables also benefit from automatic maintenance and performance optimizations.  

Databricks recommends everyone to use Managed Tables where possible. With this hierarchical object structure, you will have to use the three level namespace to access a Table, View or a Function. For example, to access a table, you will refer to catalog.schema.table name.  

![image](https://github.com/user-attachments/assets/85e3cbd3-ec56-4e8c-b644-5c45d7b9a022)

Unity Catalog also introduces two new objects called Storage Credential and External Location to access a cloud storage or a Data Lake other than the default storage configured while creating the Metastore. This is just a quick introduction to them, they'll be covered later in detail. For completeness, there are also three further objects called Share, Recipient and Provider introduced by Unity Catalog to handle Delta sharing.  
![image](https://github.com/user-attachments/assets/c9778061-0199-4db5-a50c-aa1d6aeb1286)

![image](https://github.com/user-attachments/assets/63377060-5531-4d5a-8724-59b9398d8022)

Or we can create multiple catalogs, schemas, and tables/viw within a meastore.  
![image](https://github.com/user-attachments/assets/834430b1-1139-44a0-a867-86272863aeef)

Create a table in your catalog. 
![image](https://github.com/user-attachments/assets/9f0955bb-c378-412c-9707-b87d5218b1f7)

Data will be stored in .parquet file in the storage container  
![image](https://github.com/user-attachments/assets/1039bf33-73f0-469d-a23c-9ec18cb52b52)

Query the catalog data from databricks notebook. 
![image](https://github.com/user-attachments/assets/f41a220e-65a4-4c71-9900-343e923ae853)
![image](https://github.com/user-attachments/assets/2f1c090b-0943-4433-968e-b4b2d7089665)

# Mount DBFS  
DBFS is simply a file system that provides distributed access to the data stored in Azure storage. It's not a storage solution in itself. The storage here is the Azure Blob Storage, and this is the default storage that's created when the Databricks workspace was deployed. This DBFS mount on the default Azure Blob Storage is called DBFS Root.  
![image](https://github.com/user-attachments/assets/67fa993e-614e-4f6e-aaf4-cbe279325550)

# Data Ingestion

![image](https://github.com/user-attachments/assets/5b52440b-3760-4ff2-8ad7-02b32ff19959)

# Databricks Workflow

Databricks offers jobs that you can schedule to run a specific time are a regular interval, which is great, but it lacks a lot of functionality that you would normally get with any kind of scheduling tools. For example, you can't create dependencies between jobs. To address that Databricks offers and utility called notebook utility, which lets you create notebook workflow. generally these kind of things are not done in Databricks, because of its limited capability within the scheduler itself. You'll have to write Python code like this in order to achieve concurrent execution. So instead of this in a production scenario, you would go to Azure Data Factory, because that gives you a rich set of capabilities. Like you can execute things in parallel, you can have different types of clusters for each one of them and all of that kind of stuff.

![image](https://github.com/user-attachments/assets/b2e57f01-2485-4641-a1d8-562b485b066e)

![image](https://github.com/user-attachments/assets/48838fe7-8f83-42f9-991f-c717f03e3cfa)

![image](https://github.com/user-attachments/assets/2d50cb6b-161f-4908-9384-4bf973c9b3c9)

![image](https://github.com/user-attachments/assets/ab36c7fc-608b-48c6-a1dc-c352c8f373bc)

![image](https://github.com/user-attachments/assets/2f56f890-6bbb-476d-b235-100365c19378)


# Azure Microsoft Fabric
With Microsoft Fabric, you don't have to spend all of your time combining various services from different vendors. Instead, you can use a single product that is easy to understand, set up, create, and manage. Fabric offers persona-optimized experiences and tools in an integrated user interface.
In addition to a simple, shared user experience, Fabric is a unified software-as-a-service (SaaS) offering, with all your data stored in a single open format in OneLake. OneLake is accessible by all of the analytics engines in the platform. Fabric offers scalability, cost-effectiveness, accessibility from anywhere with an internet connection, and continuous updates and maintenance provided by Microsoft.

**Explore OneLake**  
OneLake is Fabric's lake-centric architecture that provides a single, integrated environment for data professionals and the business to collaborate on data projects. Fabric's OneLake architecture facilitates collaboration between data team members and saves time by eliminating the need to move and copy data between different systems and teams. OneCopy is a key component of OneLake that allows you to read data from a single copy, without moving or duplicating data.  
Think of it like OneDrive for data; OneLake combines storage locations across different regions and clouds into a single logical lake, without moving or duplicating data. Similar to how Office applications are prewired to use your organizational OneDrive, all the compute workloads in Fabric are preconfigured to work with OneLake. Fabric's data warehousing, data engineering (lakehouses and notebooks), data integration (pipelines and dataflows), real-time intelligence, and Power BI all use OneLake as their native store without needing any extra configuration.

![image](https://github.com/user-attachments/assets/20878605-ffe7-4e56-94aa-148d65c78b88)

OneLake is built on top of Azure Data Lake Storage (ADLS) and data can be stored in any format, including Delta, Parquet, CSV, JSON, and more.  

What this means is that all of the compute engines in Fabric automatically store their data in OneLake. Data that is stored in OneLake is then directly accessible by all of the compute engines without needing to be moved or copied. For tabular data, the analytical engines in Fabric write data in delta-parquet format and all engines interact with the format seamlessly.  

One important feature of OneLake is the ability to create shortcuts, which are embedded references within OneLake that point to other files or storage locations. Shortcuts allow you to quickly source your existing cloud data without having to copy it, and enables Fabric experiences to derive data from the same source to always be in sync.  

![image](https://github.com/user-attachments/assets/ba7e1900-592d-4dc0-9cef-78f7bf130b2e)

**Explore Fabric's experiences**  
Fabric offers a set of analytics experiences that are designed to accomplish specific tasks and work together seamlessly. Fabric's experiences include:  

**Synapse Data Engineering:** data engineering with a Spark platform for data transformation at scale.  
**Synapse Data Warehouse:** data warehousing with industry-leading SQL performance and scale to support data use.  
**Synapse Data Science:** data science with Azure Machine Learning and Spark for model training and execution tracking in a scalable environment.  
**Synapse Real-Time Intelligence**: real-time intelligence to query and analyze large volumes of data in real-time.  
**Data Factory:** data integration combining Power Query with the scale of Azure Data Factory to move and transform data.  
**Power BI:** business intelligence for translating data to decisions through interactive reports.  
Fabric provides a comprehensive data analytics solution by unifying all these experiences on a single platform.  

**Explore workspaces**  
Fabric uses workspaces to contain the different items created across the different experiences. Each organization can customize how to separate and control access to the items. Some possibilities include a dedicated workspace for lakehouse development and a separate workspace for the production lakehouse.  

In **Microsoft Fabric**, workspaces serve as logical containers that help you organize and manage your data, reports, and other assets. They provide a clear separation of resources, making it easier to control access and maintain security. Each workspace can have its own set of permissions, ensuring that only authorized users can view or modify the contents. This structure supports collaboration within teams while maintaining strict access control, which is crucial for both business and IT users.  

Workspaces in Microsoft Fabric also offer settings to manage compute resources and integrate with Git for version control. You can configure compute settings to optimize performance and cost, ensuring that your resources are used efficiently. Git integration allows you to track changes, collaborate on code, and maintain a history of your work, which is essential for development and data management. Additionally, workspaces support features like data lineage and impact analysis, providing a comprehensive view of data flow and dependencies, which enhances transparency and decision-making.  

**Explore security and governance**  
Fabric's OneLake is centrally governed and open for collaboration. Data is secured and governed in one place, which allows users to easily find and access the data they need. Fabric administration is centralized in the admin center.  

In the admin center you can manage groups and permissions, configure data sources and gateways, and monitor usage and performance. You can also access the Fabric admin APIs and SDKs in the admin center, which you'd use to automate common tasks and integrate Fabric with other systems.  

**Evolution of collaborative workflows**  
Microsoft Fabric transforms the analytics development process by unifying tools into a SaaS platform, allowing flexibility for different roles to perform necessary skills without duplicating efforts.  

**Data engineers** can now ingest, transform, and load large amounts of data into OneLake and present it in whichever data store makes most sense. Data loading patterns are simplified using pipelines and architectures, such as medallion, can be easily configured using workspaces.  
**Data analysts** gain greater context and streamline processes, transforming data upstream with Data Factory and connecting with data more directly using DirectLake mode.  
**Data scientists** Integrate native data science techniques more easily and use Power BI's interactive reporting to provide data-informed insights.  
**Analytics engineers** bridge the gap between data engineering and data analysis by curating data store assets, ensuring data quality, and enabling self-service analytics.  
**Low-to-no-code** users and citizen developers can now discover curated data through the OneLake hub, and further process and analyze it to suit their needs without being dependent on data engineers or duplicating data.  
**Enable Microsoft Fabric**  
If you have admin privileges, you can access the Admin center from the Settings menu in the upper right corner of the Power BI service. From here, you enable Fabric in the Tenant settings.
**Admins** can make Fabric available to either the entire organization or specific groups of users, who can be organized based on their Microsoft 365 or Microsoft Entra security groups. Admins can also delegate the ability to enable Fabric to other users, at the capacity level.  

**Create workspaces**  
Workspaces are collaborative environments where you create and manage items like lakehouses, warehouses, and reports. All data is stored in OneLake, and is accessed through workspaces. Items are displayed in a list or lineage view, which is a visual representation of the dependency between items.  

In the Workspace settings, you can configure the license type to use Fabric features. There are several other settings you can configure in this area, some of which include:  
OneDrive access for the workspace  
Azure Data Lake Gen2 Storage connection  
Integration with Git for version control  
Spark workload settings  

![image](https://github.com/user-attachments/assets/f566ea70-f7db-49fc-a0d7-947da4d0d7d4)

![image](https://github.com/user-attachments/assets/481cde68-8b13-4735-8fdd-05d89d2a0c7b)

**Create items in Fabric**
After you create your Fabric enabled workspace, you can start creating items in Fabric. You can create items in Fabric using the Create menu in the upper left corner of the Power BI service.
![image](https://github.com/user-attachments/assets/21d7a67b-96ca-4d16-8f50-3eea1da3fbbf)

**Knowledge Check**
![image](https://github.com/user-attachments/assets/7e70da1b-9308-4001-a6da-ed2c44822948)




