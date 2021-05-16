# DP 200 - Implementing a Data Platform Solution
# Lab 3 - Enabling Team Based Data Science with Azure Databricks

**Estimated Time**: 75 minutes

**Pre-requisites**: It is assumed that the case study for this lab has already been read. It is assumed that the content and lab for module 1: Azure for the Data Engineer has also been completed

**Lab files**: The files for this lab are located in the _Allfiles\Labfiles\Starter\DP-200.3_ folder.

## Lab overview

By the end of this lab the student will be able to explain why Azure Databricks can be used to help in Data Science projects. The students will provision an Azure Databricks instance and will then create a workspace that will be used to perform simple data preparation tasks from a Data Lake Store Gen2 store. Finally, the student will perform a walk-through of performing transformations using Azure Databricks.

## Lab objectives
  
After completing this lab, you will be able to:

1. Explain Azure Data Lake Storage
2. Upload data into Azure Data Lake
3. Worked with Azure Databricks
4. Read data with Azure Databricks
5. Performed transformations with Azure Databricks

## Scenario
  
In response to the Information Services (IS) department, you will start the process of building a predictive analytics platform by listing out the benefits of using the technology. The department will be joined by data scientists and they want to ensure that there is a predictive analytics environment available to the new team members.

You will stand up and provision an Azure Databricks environment, and then test that this environment works by performing a simple data preparation routine on the service by ingesting data from a pre-existing Data Lake Storage Gen2 account. As a data engineer, it has been indicated to you that you may be required to help the data scientists perform data preparation exercises. To that end, you have been recommended to walk-through a notebook that can help you perform basic transformations.

At the end of this lad, you will have:

1. Explain Azure Data Lake Storage
2. Upload data into Azure Data Lake
3. Worked with Azure Databricks
4. Read data with Azure Databricks
5. Performed transformations with Azure Databricks

## Exercise 1: Explain Azure Data Lake Storage
  
Estimated Time: 15 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Create and configure a storage account named **awdlsstudxx** as a Data Lake Store Gen2 storage type in the region closest to the lab location, within the resource group awrgstudxx, where **xx** are your initials.

2. Create containers named **logs** and **data** within the awdlsstudxx storage account.


### Task 1: Create and configure a storage account as a Data Lake Store Gen II store.

1. In the Azure portal, click on **+ Create a resource** icon.

2. In the New screen, click in the **Search the Marketplace** text box, and type the word **storage**. Click **Storage account** in the list that appears.

3. In the **Storage account** blade, click **Create**.

4. From the **Create storage account*** blade, create a storage account with the following settings:

    - Under the project details, specify the following settings:

        - **Subscription**: the name of the subscription you are using in this lab
    
        - **Resource group name**: **awrgstudxx**, where **xx** are your initials.

    - Under the instance details, specify the following settings:

        - **Storage account name**: **awdlsstudxx**, where **xx** are your initials.

        - **Location**: the name of the Azure region which is closest to the lab location and where you can provision Azure VMs.

        - **Performance**: **Standard**.

        - **Account kind**: **StorageV2 (general purpose v2)**.

        - **Replication**: **Read-access geo-redundant storage (RA_GRS)**

5. Click on the **Advanced** tab.

6. Under Data Lake Storage Gen2, click **Enabled** under **Hierarchical namespace**.

    ![Defining the Hierarchical Namespace setting in Create Storage Account screen in the Azure portal](Linked_Image_Files/M02-E03-T01-img01.png)

7. In the **Create storage account** blade, click **Review + create**.

8. After the validation of the  **Create storage account*** blade, click **Create**.

   > **Note**: The creation of the storage account will take approximately 90 seconds while it provisions the disks and the configuration of the disks as per the settings you have defined.

### Task 2: Create and configure a Container within the storage account.

1. In the Azure portal, a message states that _Your deployment is complete_, click on the button **Go to resource**.

2. In the **awdlsstudxx** screen, where **xx** are your initials, click **Containers**.

3. In the **awrgstudxx - Containers** screen, at the top left, click on the  **+ Containers** button.

4. From the **New** screen, create two containers with the following name:

    - Name: **data** with the public access level of **Private (no anonymous access)**.

    - Name: **logs** with the public access level of **Private (no anonymous access)**.

5. In the **New Containers** screen, click **Create**.

   > **Note**: The creation of the file system is immediate and will appear in the list of the **awdlsstudxx - Containers** screen as follows.

    ![File Systems listed in the Azure portal](Linked_Image_Files/M02-E03-T02-img01.png)

> **Result**: After you completed this exercise, you have created a Data Lake Gen2 Storage account named awdlsstudxx that has a file system named data and logs.

## Exercise 2: Upload data into Azure Data Lake.
  
Estimated Time: 10 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Install and start Microsoft Azure Storage Explorer

2. Upload some data files to the containers of the Data Lake Gen II Storage Account.

### Task 1: Install Storage Explorer.

3. In the Azure portal, in the **awdlsstudxx** overview page, navigate to **Open in Explorer** and then click on the **Download Azure Storage Explorer** hyperlink.

4. You are taken to the following web page for [Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/) where there is a button that states **Download now**. click on this button.

5. In the Microsoft Edge dialog box click **Save**, when the download is complete, click on **View downloads**, in the download screen in Microsoft Edge, click on **Open folder**. This will open the Downloads folder.

6. Double click the file **StorageExplorer.exe**, in the User Account Control dialog box click on **Yes**.

7. In the License Agreement screen, select the radio button next to **I agree the agreement**, and then click on **Install**.

   > **Note**: The installation of Storage Explorer can take approximately 4 minutes. Azure Storage Explorer allows you to easily manage the contents of your storage account with Azure Storage Explorer. Upload, download, and manage blobs, files, queues, tables, and Cosmos DB entities. It also enables you to gain easy access to manage your virtual machine disks.

8. On completion of the installation, ensure that the checkbox next to **Launch Microsoft Azure Storage Explorer** is selected and then click **Finish**. Microsoft Azure Storage Explorer opens up and lists your subscriptions.

9. In Storage Explorer, select **Manage Accounts** to go to the **Account Management Panel**.

10. The left pane now displays all the Azure accounts you've signed in to. To connect to another account, select **Add an account**

11. If you want to sign into a national cloud or an Azure Stack, click on the Azure environment dropdown to select which Azure cloud you want to use. Once you have chosen your environment, click the **Sign in...** button.

12. After you successfully sign in with an Azure account, the account and the Azure subscriptions associated with that account are added to the left pane. Select the Azure subscriptions that you want to work with, and then select **Apply**. The left pane displays the storage accounts associated with the selected Azure subscriptions.

    ![Azure Storage Explore](Linked_Image_Files/M02-E04-T01-img01.png)

### Task 2: Upload data files to the data and logs container of the Data Lake Gen II Storage Account.

1. In Azure Storage Explorer, click on the arrow to expand your subscription.

2. Under **Storage Accounts**, search for the storage account **awdlsstudxx (ADLS Gen2)**, and click on the arrow to expand it.

3. Under **Blob Containers**, click on the arrow to expand it and show the **logs** file system. Click on the **logs** file system.

4. In Azure Storage Explorer, click on the arrow next to the **Upload** icon, and click on the **Upload Files..**.

5. In Upload Files dialog box, click on the ellipsis next to the **Selected files** text box.

6. In the **Choose files to upload** dialog box, browse to **Labfiles\Starter\DP-200.2\logs** folder. Highlight the following files:

    - weblogsQ1.log

    - weblogsQ2.log

    - preferences.json

7. In the **Choose files to upload** dialog box, click **Open**.

8. In the **Upload Files** screen, click on the **Upload** button.

   ![Uploading files in Azure Storage Explore](Linked_Image_Files/M02-E04-T02-img01.png)

9. Under **Blob Containers**, click on the arrow to expand it and show the **data** file system. Click on the **data** file system.

10. In Azure Storage Explorer, click on the arrow next to the **Upload** icon, and click on the **Upload Files..**.

11. In Upload Files dialog box, click on the ellipsis next to the **Selected files** text box.

12. In the **Choose files to upload** dialog box, browse to **Labfiles\Starter\DP-200.2\Static Files** folder. Highlight the following files:

    - DimDate2.txt

13. In the **Choose files to upload** dialog box, click **Open**.

14. In the **Upload Files** screen, click on the **Upload** button.

15. Repeat the steps to upload the preferences.JSON file from the **Labfiles\Starter\DP-200.2\logs** folder to the **data** file system in the Data Lake Store gen2

   > **Note**: The upload of the files will take approximately 5 seconds. You will see a message in Azure Storage Explorer that states **Your view may be out of data. Do you want to refresh? Click Yes**. Once completed, all two files will appear in a list in the upload blobs screen.

    ![Files uploaded to Containers in Azure Storage Explore](Linked_Image_Files/M02-E04-T02-img02.png)

16. In Azure Storage Explorer, in the data file system, click on the **+ New Folder** button.

17. In the New Folder screen, in the New folder name text box, type **output**.

18. Close down Azure Storage Explorer.

19. Return to the Azure portal, and navigate to the **Home** blade.

> **Result**: After you completed this exercise, you have created a Data Lake Gen II Storage account named awdlsstudxx that has a file system named data that contains two weblog files that are ready to be used by the Data scientists at AdventureWorks.


## Exercise 3: Work with Azure Databricks
  
Estimated Time: 20 minutes

Individual exercise
  
The main tasks for this exercise are as follows:

1. Create an Azure Databricks Premium Tier instance in a resource group.

2. Open Azure Databricks

3. Launch a Databricks Workspace and create a Spark Cluster

### Task 1: Create and configure an Azure Databricks instance.

1. In the Azure portal, at the top left of the screen, click on the **Home** hyperlink.

2. In the Azure portal, click on the **+ Create a resource** icon.

3. In the New screen, click in the **Search the Marketplace** text box, and type the word **databricks**. Click **Azure Databricks** in the list that appears.

4. In the **Azure Databricks** blade, click **Create**.

5. In the **Azure Databricks Service** blade, create an Azure Databricks Workspace with the following settings:

    - **Workspace name**: **awdbwsstudxx**, where **xx** are your initials.

    - **Subscription**: the name of the subscription you are using in this lab

    - **Resource group**: **awrgstudxx**, where **xx** are your initials.

    - **Location**: the name of the Azure region which is closest to the lab location and where you can provision Azure VMs.

    - **Pricing Tier**: **Premium (+ Role-based access controls)**.


        ![Creating Azure Databricks in the Azure portal](Linked_Image_Files/M03-E02-T01-img01.png)

6. In the **Azure Databricks Service** blade, click **Create**.

   > **Note**: The provision will take approximately 3 minutes. The Databricks Runtime is built on top of Apache Spark and is natively built for the Azure cloud. Azure Databricks completely abstracts out the infrastructure complexity and the need for specialized expertise to set up and configure your data infrastructure. For data engineers, who care about the performance of production jobs, Azure Databricks provides a Spark engine that is faster and performant through various optimizations at the I/O layer and processing layer (Databricks I/O).
   
### Task 2: Open Azure Databricks.

1. Confirm that the Azure Databricks service has been created.

2. In the Azure portal, navigate to the **Resource group** screen.

3. In the Resource groups screen, click on the ****awrgstudxx** resource group, where **xx** are your initials.

4. In the **awrgstudxx** screen, click **awdbwsstudxx**, where **xx** are your initials to open Azure Databricks. This will open your Azure Databricks service.

    ![Azure Databricks Service in the Azure portal](Linked_Image_Files/M03-E02-T02-img01.png)

### Task 3: Launch a Databricks Workspace and create a Spark Cluster.

1. In the Azure portal, in the **awdbwsstudxx** screen, click on the button **Launch Workspace**.

    > **Note**: You will be signed into the Azure Databricks Workspace in a separate tab in Microsoft Edge.

2. Under **Common Tasks**, click **New Cluster**.

3. In the **Create Cluster** screen, under New Cluster, create a Databricks Cluster with the following settings, and then click on **Create Cluster**:

    - **Cluster name**: **awdbclstudxx**, where **xx** are your initials.

    - **Cluster Mode**: **Standard**

    - **Pool**: **None**

    - **Databricks Runtime Version**: **Runtime: 8.2 (Scala 2.12, Spark 3.1.1)**
    
    - Make sure you select the **Terminate after 30** minutes of inactivity check box. If the cluster isn't being used, provide a duration (in minutes) to terminate the cluster.

    - **Min Workers**: **1**

    - **Max Workers**: **2**

    - Leave all the remaining options to their current settings.

        ![Creating an Azure Databricks Cluster in the Azure portal](Linked_Image_Files/M03-E02-T03-img01.png)

4. In the **Create Cluster** screen, click on **Create Cluster** and leave the Microsoft Edge screen open.

> **Note**: The creation of the Azure Databricks instance will take approximately 10 minutes as the creation of a Spark cluster is simplified through the graphical user interface. You will note that the **State** of **Pending** whilst the cluster is being created. This will change to **Running** when the Cluster is created.

> **Note**: While the cluster is being created, **go back and perform Exercise 1**.

## Exercise 2: Read data with Azure Databricks

Estimated Time: 30 minutes

Individual exercise

The main tasks for this exercise are as follows:

1. Confirm that the Databricks cluster has been created.

2. Collect the Azure Data Lake Store Gen2 account name

3. Enable your Databricks instance to access the Data Lake Gen2 Store.

4. Create a Databricks Notebook and connect to a Data Lake Store.

5. Read data in Azure Databricks.

### Task 1: Confirm the creation of the Databricks cluster

1. Return back to Microsoft Edge, under **Interactive Clusters** confirm that the state column is set to **Running** for the cluster named **awdbclstudxx**, where **xx** are your initials.

### Task 2: Collect the Azure Data Lake Store Gen2 account name

1. In Microsoft Edge, click on the  Azure portal tab, click **Resource groups**, and then click **awrgstudxx**, and then click on **awdlsstudxx**, where **xx** are your initials.

2. In the **awdlsstudxx** screen, under settings, click on **Access keys**, and then click on the copy icon next to the **Storage account name**, and paste it into Notepad.

    ![Accessing Data Lake Storage account name in the Azure portal](Linked_Image_Files/M03-E03-T02-img01.png)

### Task 3: Enable your Databricks instance to access the Data Lake Gen2 Store.

1. In the Azure portal, Click the **Home** hyperlink, and then click the **Azure Active Directory** icon.

2. In the **Microsoft - Overview** screen, click on **App registrations**.

3. In the **Microsoft - App registrations** screen, click on the **+ New registration** button.

4. In the register an application screen, provide the **name** of **DLAccess** and under the **Redirect URI (optional)** section, ensure **Web** is selected and type **http://localhost**for the application value. After setting the values.

    ![Registering an application in the Azure portal](Linked_Image_Files/M03-E03-T03-img01.png)

5. Click **Register**. The DLAccess screen will appear.

6. In the **DLAccess** registered app screen, copy the **Application  (client) ID** and **Directory (tenant) ID** and paste both into Notepad.

7. In the **DLAccess** registered app screen, click on **Certificates and Secrets**, and the click **+ New Client Secret**

8. In the Add a client secret screen. type a **description** of **DL Access Key**, and a **duration** of **In 1 year** for the key. When done, click **Add**.

    ![Adding a client secret in the Azure portal](Linked_Image_Files/M03-E03-T03-img02.png)

    >**Important**: When you click on **Add**, the key will appear as shown in the graphic below. You only have one opportunity to copy this key value into Notepad

    ![Location of the DLAccess Key](Linked_Image_Files/M03-E03-T03-img03.png)

9. Copy the **Application key value** and paste it into Notepad

10. Assign the Storage Blob Data Contributor permission to your resource group. In the Azure portal, click on the **Home** hyperlink, and then the **Resource groups** icon, click on the resource group **awrgstudxx**, where **xx** are your initials.

11. In the **awrgstudxx** screen, click on **Access Control (IAM)** 

12. Click on the **Role assignments** tab. 

13. Click **+ Add**, and click **Add role assignment**

14. In the **Add role assignment** blade, under Role, select **Storage Blob Data Contributor**.

15. In the **Add role assignment** blade, under Select, select **DLAccess**, and then click **Save**.

16. In the Azure portal, click the **Home** hyperlink, and then click the **Azure Active Directory** icon, Note **your role**. If you have the User role, you must make sure that non-administrators can register applications.

17. Click **Users**, and then click **User settings** in the **Users - All users** blade, Check the **App registrations** setting. This value can only be set by an administrator. If set to Yes, any user in the Azure AD tenant can register an app. 

18. Close down the **Users - All users** screen.

19. In the Azure Active Directory blade, click **Properties**.

20. Click on the Copy icon next to the **Directory ID** to get your tenant ID and paste this into notepad.

21. Save the notepad document in the folder **Allfiles\Labfiles\Starter\DP-200.3** as **DatabricksDetails.txt**

### Task 4: Create a Databricks Notebook and connect to a Data Lake Store.

1. In Microsoft Edge, click on the tab **Clusters - Databricks**

    > **Note**: You will see the Clusters page.

2. In the Azure Databricks blade on the left of Microsoft Edge, click on Under **Workspace**, click on the drop down next to **Workspace**, then point to **Create** and then click on **Notebook**.

3. In the **Create Notebook** screen, next to Name type **My Notebook**.

4. Next to the **Language** drop down list, select **Scala**.

5. Ensure that the Cluster states the name of the cluster that you have created earlier, click on **Create**

    ![Creating a Notebook in Azure Databricks](Linked_Image_Files/M03-E03-T04-img01.png)

     > **Note**: This will open up a Notebook with the title My Notebook (Scala).

6. In the Notebook, in the cell  **Cmd 1**, copy the following code and paste it into the cell:

    ```scala
    //Connect to Azure Data Lake Storage Gen2 account

    spark.conf.set("fs.azure.account.auth.type", "OAuth")
    spark.conf.set("fs.azure.account.oauth.provider.type", "org.apache.hadoop.fs.azurebfs.oauth2.ClientCredsTokenProvider")
    spark.conf.set("fs.azure.account.oauth2.client.id.<storage-account-name>.dfs.core.windows.net", "<application-id>")
    spark.conf.set("fs.azure.account.oauth2.client.secret.<storage-account-name>.dfs.core.windows.net", "<authentication-key>")
    spark.conf.set("fs.azure.account.oauth2.client.endpoint.<storage-account-name>.dfs.core.windows.net", "https://login.microsoftonline.com/<tenant-id>/oauth2/token")
    ```

7. In this code block, replace the **application-id**, **authentication-id**, **tenant-id**, **file-system-name** and **storage-account-name** placeholder values in this code block with the values that you collected earlier and are held in notepad.

8. In the Notebook, in the cell under **Cmd 1**, click on the **Run** icon and click on **Run Cell** as highlighted in the following graphic. 

    ![Running cvode in a Notebook in Azure Databricks](Linked_Image_Files/M03-E03-T04-img02.png)

    >**Note** A message will be returned at the bottom of the cell that states "Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx"

### Task 5: Read data in Azure Databricks.

1. In the Notebook, hover your mouse at the top right of cell **Cmd 1**, and click on the **Add Cell Below** icon. A new cell will appear named **Cmd2**.

    ![Adding a cell in a Notebook in Azure Databricks](Linked_Image_Files/M03-E03-T04-img03.png)

2. In the Notebook, in the cell  **Cmd 2**, copy the following code and paste it into the cell:

    ```scala
    //Read JSON data in Azure Data Lake Storage Gen2 file system

    val df = spark.read.json("abfss://<file-system-name>@<storage-account-name>.dfs.core.windows.net/preferences.json")
    ```

3. In this code block, replace the **file-system-name** with the word **logs** and **storage-account-name** placeholder values in this code block with the value that you collected earlier and are held in notepad.

4. In the Notebook, in the cell under **Cmd 2**, click on the **Run** icon and click on **Run Cell**. 

    >**Note** A message will be returned at the bottom of the cell that states that a Spark job has executed and "Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx"

5. In the Notebook, hover your mouse at the top right of cell **Cmd 2**, and click on the **Add Cell Below** icon. A new cell will appear named **Cmd3**.

6. In the Notebook, in the cell  **Cmd 3**, copy the following code and paste it into the cell:

    ```scala
    //Show result of reading the JSON file
  
    df.show()
    ```

    ![Running results in a Notebook in Azure Databricks](Linked_Image_Files/M03-E03-T04-img04.png)

7. In the Notebook, in the cell under **Cmd 3**, click on the **Run** icon and click on **Run Cell**.

    >**Note**  A message will be returned at the bottom of the cell that states that a Spark job has executed, a table of results are returned and "Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx"

8. Leave the Azure Databricks Notebook open

>**Result** In this exercise, you have performed the necessary steps that setup up the permission for Azure Databricks to access data in an Azure Data Lake Store Gen2. You then used scala to connect up to a Data Lake Store and you read data and created a table output showing the preferences of people.

## Exercise 4: Perform basic transformations with Azure Databricks

Estimated Time: 10 minutes

Individual exercise

The main tasks for this exercise are as follows:

1. Retrieve specific columns on a Dataset

2. Performing a column rename on a Dataset

3. Add an Annotation

4. If Time permits: Additional transformations

### Task 1: Retrieve specific columns on a Dataset

1. In the Notebook, hover your mouse at the top right of cell **Cmd 3**, and click on the **Add Cell Below** icon. A new cell will appear named **Cmd4**.

2. In the Notebook, in the cell  **Cmd 4**, copy the following code and paste it into the cell:

    ```scala
    //Retrieve specific columns from a JSON dataset in Azure Data Lake Storage Gen2 file system
    
    val specificColumnsDf = df.select("firstname", "lastname", "gender", "location", "page")
    specificColumnsDf.show()
    ```

3. In the Notebook, in the cell under **Cmd 4**, click on the **Run** icon and click on **Run Cell**. 

    >**Note**  A message will be returned at the bottom of the cell that states that a Spark job has executed, a table of results are returned and "Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx"

    ![Running a scala query in a Notebook in Azure Databricks](Linked_Image_Files/M03-E04-T01-img01.png)

### Task 2: Performing a column rename on a Dataset

1. In the Notebook, hover your mouse at the top right of cell **Cmd 4**, and click on the **Add Cell Below** icon. A new cell will appear named **Cmd5**.

2. In the Notebook, in the cell  **Cmd 5**, copy the following code and paste it into the cell:

    ```scala
    //Rename the page column to bike_preference

    val renamedColumnsDF = specificColumnsDf.withColumnRenamed("page", "bike_preference")
    renamedColumnsDF.show()
    ```

3. In the Notebook, in the cell under **Cmd 5**, click on the **Run** icon and click on **Run Cell**. 

    >**Note**  A message will be returned at the bottom of the cell that states that a Spark job has executed, a table of results are returned and "Command took 0.0X seconds -- by person at 4/4/2019, 2:46:48 PM on awdbclstudxx"

    ![Renaming columns in a query in a Notebook in Azure Databricks](Linked_Image_Files/M03-E04-T02-img01.png)

### Task 3: Adding Annotations

1. In the Notebook, hover your mouse at the top right of cell **Cmd 5**, and click on the **Add Cell Below** icon. A new cell will appear named **Cmd6**.

2. In the Notebook, in the cell  **Cmd 6**, copy the following code and paste it into the cell:

    ```text
    This code connects to the Data Lake Storage filesystem named "Data" and reads data in the preferences.json file stored in that data lake. Then a simple query has been created to retrieve data and the column "page" has been renamed to "bike_preference".
    ```

3. In the Notebook, in the cell under **Cmd 6**, click on the **down pointing arrow** icon and click on **Move up**. Repeat until the cell appears at the top of the Notebook.

4. Leave the Azure Databricks Notebook open

    >**Note**  A future lab will explore how this data can be exported to another data platform technology

> **Result**: After you completed this exercise, you have created an annotation within a notebook.

