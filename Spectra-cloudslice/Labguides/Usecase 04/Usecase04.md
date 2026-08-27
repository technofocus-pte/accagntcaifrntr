<!--
lab:
  title: Usecase 04 - Build a customer resolution agent grounded with Work IQ, Foundry IQ, and Fabric IQ
  description: In this task, you will create a Foundry resource which is required to access the Microsoft Foundry.
  duration: 10 minutes
  level: 400
  islab: true
  primarytopics:
    - Microsoft Foundry
-->

# Usecase 04 - Build a customer resolution agent grounded with Work IQ, Foundry IQ, and Fabric IQ

## Introduction

This use case focuses on building an intelligent **customer resolution agent** for Contoso Electronics by integrating multiple Microsoft AI capabilities, including Azure AI Search, Microsoft Fabric, and Microsoft Foundry

The solution simulates a real-world operations and support environment where customer issues such as shipment delays, refunds, and escalations are handled using AI-driven insights. The agent leverages structured data (orders, inventory, support tickets), unstructured data (emails), and policy knowledge to provide accurate recommendations and automate responses. This creates a unified Copilot-like experience that enhances operational efficiency and customer satisfaction.

### Objectives

The main objectives of this use case are:
- To create and configure an **Azure AI Search** service for indexing
  and retrieving enterprise documents.

- To set up a **storage account** and ingest policy and operational
  documents for knowledge grounding.

- To build a **Foundry Agent** that acts as a customer support and
  operations assistant.

- To create a **Microsoft Fabric workspace and lakehouse** for storing
  and managing business data such as customers, orders, and shipments.

- To design an **Ontology model** that defines relationships between
  entities like Customers, Orders, Support Tickets, and Refund Claims.

- To develop a **Fabric Data Agent** that can interpret business data
  and provide insights.

- To integrate **Work IQ (email), Foundry IQ (policies), and Fabric IQ
  (data)** into a unified agent.

- To enable the agent to:

    - Analyze customer issues
    - Validate data across systems
    - Apply business policies
    - Recommend resolutions
    - Generate professional responses


### Task 1: Create an Azure AI Search resource

In this exercise, you will create an Azure AI Search resource from the Azure portal. This will be used to search the documents using AI capability.

**Azure AI Search** is a cloud-based service for searching within your privately curated data. It uses a combination of Microsoft’s AI and JSON-based indexes to provide fast, relevant search results.

1. Open a browser and login to Azure portal at +++https://portal.azure.com/+++ with your credentials.

    - Username - +++@lab.CloudPortalCredential(User1).Username+++
    - Password - +++@lab.CloudPortalCredential(User1).AccessToken+++

    ![Enter Your Username](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image1.png)

    ![Enter Your Password](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image2.png)


1. From the Home page of the Azure portal, select **Microsoft Foundry** and select **Microsoft Foundry** under Services.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image3.png)

1. In the **Misrosoft Foundry page**, select **AI Search** under **Use with Foundry** from the left pane and then select **+ Create**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image4.png)

1. Enter the below details and select **Review + create (4)**.

    - Subscription - Select your **assigned subscription**
    - Service name - **searchleaves2306402 (1)**
    - Resource group - **AgenticAI (2)**
    - Location - **Central US (3)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image5.png)


1. Once the validation passes, select **Create**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image6.png)

1. The deployment takes around 10 minutes to complete. Select **Go to resource** once the search service is created.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image7.png)

1. From the **Overview** page, copy the **Url** value and save it in a notepad to be used in a future exercise.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image8.png)

1. Select **Keys (1)** under **Settings + networking** from the left pane. Copy the **Primary admin key (2)** and save it in a notepad for using it in the upcoming exercises.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image9.png)

1. Select **Identity (1)** under **Settings + networking** from the left pane.

1. Toggle the Status to **On (2)** under **System assigned** and then click on **Save (3)**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image10.png)

1. Select **Yes** in the **Enable system assigned managed identity** confirmation dialog.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image11.png)


### Task 2: Create a Storage account

1. In the Azure portal search bar, search for **Storage accounts (1)** and select **Storage accounts (2)**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image12.png)

1. Select **+ Create** to create a new Storage account.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image13.png)

1. Enter the below details, accept the default values in the other fields and click on **Review + create (4)**.

    - Subscription - Select your **assigned subscription**
    - Resource group - **AgenticAI (1)**
    - Storage account name - **storage2306402 (2)**
    - Region - **Central US (3)**
    - Primary service - Select **Azure Blob Storage or Azure Data Lake
    Storage (4)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image14.png)


1. Once the validation passes, click on **Create**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image15.png)

1. Once the resource creation succeeds, click on **Go to resource**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image16.png)

1. Expand **Data storage (1)** and select **Containers (2)**, then click **+ Add Container (3)** to add a new container.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image17.png)

1. On New container pane, enter the Name as **document (1)** and click on **Create (2)** to create the container.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image18.png)

1. Select the created container **document** to upload the leave policy document into it.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image19.png)

1. Click on **Upload (1)** and then select **Browse for files (2)**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image20.png)

1. Select the **all documents** from **C:\Labfiles\lab file\Usecase4\Foundry** and then click on **Upload**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image21.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image22.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image23.png)

1. Navigate to the **storage2306402** Storage account (Select **Storageaccounts** from the **Home page** of the Azure portal and select **Access Control (IAM)** from the left pane. Select **Add -\> Add role assignment**).

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image24.png)

1. Search for **Storage Blob Data Reader (1)**, **select it (2)** and click on **Next (3)**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image25.png)

1. Click on **+Select members**, search for and select your **credentails**.Username and then click on **Select**. This adds the Storage Blob Data Reader role to your user id.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image26.png)

1. Select **Managed identity (1)** and then select **+ Select members (2)**. Select **Search service (3)** under **Managed identity** and select the **searchleaves (4)** search service that gets listed, then click on **Select (5)**.

1. Select **Review + assign (6)** .

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image27.png)

1. Click on **Review & Assign** to assign the roles

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image28.png)


### Task 3: Create Foundry resource

In this task, you will create a Foundry resource which is required to access the Microsoft Foundry.

1. From the Home page of the Azure portal +++https://portal.azure.com/+++, select **Foundry**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image29.png)

1. Select **Foundry** from the left pane, and then select **+ Create** to create the Foundry resource.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image30.png)

1. Enter the below details and select **Review + create (5)**.

    - Resource group - **AgenticAI (1)**
    - Name - **+++agentic-2306402+++ (2)**
    - Region - Keep region as default
    - Default project name- **+++agentic-ai-project-2306402+++ (4)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image31.png)


1. Select **Create** once validated.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image32.png)

1. Ensure that the resource is created.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image33.png)

1. Navigate to your **AgenticAI** resource group

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image34.png)

1. Open the **agentic-ai-project-2306402** and select **Go to Foundry portal**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image35.png)

1. Click **Go to Foundry portal**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image36.png)

1. In the top navigation, select **Build**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image37.png)

    >[!Note] If you are getting permission issues follow the below steps.

    - Navigate to resource group **AgenticAI** resource group.
    - select **Add role assignement** from the **+ Add** dropdown
    under **Acess control (IAM)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image38.png)

    - Search **Foundry User** and **select from the list (2)** and
    click on **Next (3)**.

    - Click on **+Select members**, search for and select your **user
    name**, .Username and then click on **Select** and click **Review + assign** twice.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image40.png)


1. Navigate to the **Agents** page **(1)**, click **New agent** **(2)**, and then select **Build an agent** **(3)** to create a new agent using the visual builder.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image41.png)

1. Enter +++IQAgent+++ **(1)** as the agent name, and then click **Create and open playground** **(2)** to create the agent and launch the playground.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image42.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image43.png)


### Task 4: Create a Fabric workspace

In this task, you create a Fabric workspace. The workspace contains all the items needed for this lakehouse tutorial, which includes lakehouse, dataflows, Data Factory pipelines, the notebooks, Power BI datasets, and reports.

1. Open your browser, navigate to the address bar, and type or paste the following URL: +++https://app.fabric.microsoft.com/+++ then press the **Enter** button and sign in with your credentials

    - Username - +++@lab.CloudPortalCredential(User1).Username+++
    - Password - +++@lab.CloudPortalCredential(User1).AccessToken+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image44.png)


1. If PowerBI opens by default , please folllow the below steps , other wise skip this step

    - Click on PowerBI

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image45.png)

    - Select Fabric from the option

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image46.png)


1. In the Workspaces pane, click on **+ New workspace** tile

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image47.png)

1. In the **Create a workspace** pane that appears on the right side, enter the following details, and click on the **Apply** button.

    - Name: +++Fabric IQ Ontology-2306402+++ (1)**
    - Expand the **Advanced (2)** section to configure additional
    workspace settings.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image48.png)


1. Select the **Fabric** as workspace type +++(1)+++, choose the appropriate **capacity-2306402** **(2)**, ensure **Small semantic model storage format** **(3)** is selected, and then click **Apply** **(4)** to create the workspace.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image49.png)


### Task 5: Create a lakehouse

1. Create a new lakehouse by clicking on the **+New item** button in the navigation bar.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image50.png)

1. Filter by, and select, the **Lakehouse** tile.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image51.png)

1. In the **New lakehouse** dialog box, enter +++IQ_Lakehouse+++ in the **Name** field and **unselect** the lakehouses schemas. Click on the **Create** button and open the new lakehouse.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image52.png)

1. You will see a notification stating **Successfully created SQL endpoint**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image53.png)


### Task 6: Ingest sample data

1. In the **IQ_Lakehouse** page, navigate to **Get data in your lakehouse** section, and click on **Upload files as shown in the below image.**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image54.png)

1. On the Upload files tab, click on the folder under the Files

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image55.png)

1. Browse to **C:\LabFiles\lab file\Usecase 4\Fabric (1)** on your VM, then select **all csv (2)** files and click on **Open (3)** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image56.png)

1. Then, click on the **Upload** button and close the **Upload files** dialog by selecting the **X** icon for the dialog.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image57.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image58.png)

1. Click and select refresh on the **Files**. The file appear.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image59.png)

1. In the **Lakehouse** page, under the Explorer pane select **Files**. Now, hover your mouse over the **Customer.csv** file. Click on the horizontal ellipses **(…)** beside **Customer.csv**. Navigate and click on **Load Table**, then select **New table**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image60.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image61.png)

1. In the **Load file to new table** dialog box, click on the **Load** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image62.png)

1. Now successfully created **Customer** table

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image63.png)

1. Repeat Steps 6 through 9 to push the remaining file into the tables.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image64.png)

1. From the left navigation bar, select **Fabric IQ Ontology**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image65.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image66.png)


### Task 7: Create ontology (preview) item

1. In your Fabric workspace, select **+ New item**. Search for and select the **Ontology (preview)** item.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image67.png)

    >[!Note] In some cases, the “Ontology (preview)” item may not appear immediately in the “+ New item” search results. If this occurs, sign out of the Fabric portal, sign in again, and retry the search.

1. Enter +++NetworkOperationsOntology+++ **(1)** as the ontology name, verify the workspace location, and then click **Create** **(2)** to create the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image68.png)

    >[!Note] Ontology names can include numbers, letters, and underscores. Don't use spaces or dashes.

1. The ontology opens when it's ready.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image69.png)

    >[!Note] If you still face issues in loading the tables, restart the Fabric Capcity from the Azure portal.

1. Next, create entity types, data bindings, and relationships based on data from your lakehouse tables.


### Task 8: Create Entity Types and Data Bindings

Entity types represent categories of objects in your business domain. For this schema, you will create two entity types: +++Tickets+++ and **Inspections**.

1. From the top ribbon or the center of the configuration canvas, select **Add entity type**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image70.png)

1. Enter +++Customer+++ as the name and select **Add Entity Type**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image71.png)

1. On the configuration canvas, select **(...) (1)** next to the entity name and select **Bind data (2)**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image72.png)

1. Select **Add data binding (1) \> Lakehouse table (2)**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image73.png)

1. Select the **IQ_Lakehouse** lakehouse **(1)** as the data source, and then click **Next** **(2)** to continue configuring the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image74.png)

1. Expand the **Tables** folder **(1)** under **IQ_Lakehouse**, select the **customers** table **(2)**, and then click **Select** **(3)** to add the table to the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image75.png)

1. Select **Define entity type key** at the top of the configuration.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image76.png)

1. Select **customer_id** as the key property and select **Save**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image77.png)

1. Click on **Save** to save the data binding.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image78.png)

1. Confirm that the entity type updated successfully, then select **Cancel** to close the configuration options.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image79.png)

1. Click on **Home** .

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image80.png)

1. Select **+ Add entity type** from the ribbon.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image81.png)

1. Follow the same steps that you used for the **Store** entity type to create the entity types described in the following table. Each entity has a static data binding with the default columns from its source table.

    | Entity Type Name | Source Table in IQ_Lakehouse | Entity Type Key |
    |------------------|------------------------------|-----------------|
    | Order | Orders | OrderId |
    | OrderItem | OrderItems | OrderItemID |
    | SupportTicket | SupportTickets | TicketID |
    | RefundClaim | RefundClaims | ClaimID |
    | ShipmentTrackingEvent | shipmenttracking | TrackingID |


### Task 9: Create relationship types

Next, create relationship types between the entity types to represent contextual connections in your data.

1. Select the Customer entity type from the Explorer, then select **Add Relationship** from the menu ribbon.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image82.png)

1. Enter the following relationship type details and then click **Create (4)**.

    - **Relationship type name**: **+++Places+++ (1)**
    - **Source entity type**: **Customer (2)**
    - **Target entity type**: **Order (3)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image83.png)


1. The relationship is added to the semantic canvas. Select **View Relationship Type details** to open the relationship details configuration. Observe the sections of the configuration page

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image84.png)

1. In the middle section, enter the following details.

    - Mapping table: Select **customers** table from the drop-down
    - Browse available sources and select the customers table. This
    table in the source data can link **customer_id** entities together.

    - Then **Save** the relationship type.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image85.png)


1. Click **Home** to return to the ontology home page after verifying the relationship between the **Customer** and **Order** entities.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image86.png)

1. Select the **Order** entity type +++(1)+++ from the **Explorer** pane, and then click **+ Add relationship** **(2)** to define a new relationship for the selected entity.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image87.png)

1. Enter the following relationship type details and then click **Create (4)**.

    - **Relationship type name**: **+++Contains+++ (1)**
    - **Source entity type**: **Order (2)**
    - **Target entity type**: **OrderItem (3)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image88.png)


1. Click **View Relationship Type details** to review and manage the relationships defined between the entity types in the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image89.png)

1. Select **orderitems** as the **Mapping table** **(1)**, set **OrderID** **(2)** and **OrderItemID** **(3)** as the matching keys, click **Save** **(4)** to create the relationship, and then select **Home** **(5)** to return to the ontology home page.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image90.png)

1. Select the **Order** entity type +++(1)+++ from the **Explorer** pane, and then click **+ Add relationship** **(2)** to define a new relationship for the selected entity.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image87.png)

1. Enter the following relationship type details and then click **Create (4)**.

    - **Relationship type name**: **+++hasSupportTicket+++ (1)**
    - **Source entity type**: **Order (2)**
    - **Target entity type**: **SupportTicket (3)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image91.png)


1. Click **View Relationship Type details** to review and manage the relationships defined between the entity types in the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image89.png)

1. Select **supporttickets** as the **Mapping table** **(1)**, set **TicketID** for both the **Matched Order: OrderID** **(2)** and **Matched SupportTicket: TicketID** **(3)** fields, click **Save** **(4)** to create the relationship, and then select **Home** **(5)** to return to the ontology home page.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image92.png)

1. Select the **Order** entity type +++(1)+++ from the **Explorer** pane, and then click **+ Add relationship** **(2)** to define a new relationship for the selected entity.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image87.png)

1. Enter the following relationship type details and then click **Create (4)**.

    - **Relationship type name**: **+++hasTrackingEvent+++ (1)**
    - **Source entity type**: **Order (2)**
    - **Target entity type**: **ShipmentTrackingEvent (3)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image93.png)


1. Click **View Relationship Type details** to review and manage the relationships defined between the entity types in the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image89.png)

1. Select **shipmenttracking** as the **Mapping table** **(1)**, set **OrderID** **(2)** and **TrackingID** **(3)** as the matching keys, click **Save** **(4)** to create the relationship, and then select **Home** **(5)** to return to the ontology home page.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image94.png)

1. Select the **OrderItem** entity type +++(1)+++ from the **Explorer** pane, and then click **+ Add relationship** **(2)** to define a new relationship for the selected entity.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image95.png)

1. Enter the following relationship type details and then click **Create (4)**.

    - **Relationship type name**: **+++mayLeadTo+++ (1)**
    - **Source entity type**: **OrderItem (2)**
    - **Target entity type**: **RefundClaim (3)**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image96.png)


1. Click **View Relationship Type details** to review and manage the relationships defined between the entity types in the ontology.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image89.png)

1. Select **refundclaims** as the **Mapping table** **(1)**, set **OrderID** **(2)** and **ClaimID** **(3)** as the matching keys, click **Save** **(4)** to create the relationship, and then select **Home** **(5)** to return to the ontology home page.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image97.png)


### Task 10: Create data agent with ontology (preview) source

Follow these steps to create a new data agent that connects to your ontology (preview) item.

1. Now, click on **Fabric IQ Ontology** on the left-sided navigation pane.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image98.png)

1. In the **Fabric** home page, select **+New item.** In the Filter by item type search box, enter **data agent** and select the Data agent.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image99.png)

1. Enter +++IQ_Agent+++ as the Data agent name and select **Create**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image100.png)

1. In **FabricDataAgent** page, select **Add a data source**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image101.png)

1. In the OneLake catalog tab, select the **NetworkOperationsOntology** Ontology and select **Add.**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image102.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image103.png)

1. Select **Agent instructions** to configure and customize the behavior of the agent.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image104.png)

1. Enter the following data into the +++Instructions+++ section, then select **Publish**.

    ```
    You are a customer operations and order resolution analytics agent.

    Your purpose is to help answer business questions related to:
    - customer orders
    - shipment issues
    - support escalations
    - refund or replacement claims
    - fulfillment delays
    - product availability
    - account history and trends

    Use business-friendly language and provide concise but useful answers.

    Interpret the data using these business concepts:
    - A customer can place many orders.
    - An order can contain multiple products.
    - An order can have shipment incidents, tracking events, support tickets, and refund claims.
    - A customer can also have account notes that provide relationship or operational context.
    - Inventory reflects current stock availability by SKU and warehouse.

    Use these tables/concepts for the following question types:

    1. Customer and order history
    - Use Customers, Orders, OrderItems, and AccountNotes.
    - When asked about a customer’s background, summarize recent orders, important account notes, and notable support or shipment history.

    2. Shipment and delivery issues
    - Use Orders, ShipmentIncidents, ShipmentTracking, and SupportTickets.
    - When asked about delays, damaged shipments, shortages, or delivery problems, prioritize these sources.

    3. Refunds and replacements
    - Use RefundClaims, ShipmentIncidents, SupportTickets, and Orders.
    - When asked whether a refund or replacement is appropriate, look for shipment issues, customer complaints, and prior claim patterns.

    4. Product and stock availability
    - Use Inventory and OrderItems.
    - When asked whether a replacement can be fulfilled, check whether the requested SKU is available in stock.

    5. Trend and historical analysis
    - Use Orders, ShipmentIncidents, RefundClaims, SupportTickets, and ShipmentTracking.
    - When asked for trends, summarize patterns by month, issue type, customer, or product where appropriate.

    Important interpretation rules:
    - “Issue”, “problem”, or “complaint” may refer to shipment incidents, support tickets, or refund claims.
    - “Replacement” and “reshipment” should be treated as operational recovery actions.
    - “Escalation” usually refers to urgent or unresolved support or delivery issues.
    - “High-risk customer” may indicate repeated shipment issues, open tickets, unresolved claims, or negative account notes.
    - “Historical trend” means analysis over time, usually by month unless otherwise specified.

    Response guidance:
    - Prefer summaries over raw data dumps.
    - If the user asks for trends, provide a short interpretation in addition to the numbers.
    - If there is insufficient data, clearly say so.
    - If multiple records exist, prioritize the most recent and most severe items.
    - If asked for a recommendation, provide a business-oriented recommendation based on the available evidence.

    Support group by in GQL 
    ```

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image105.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image106.png)

1. After publishing, verify the success message and select **View publishing details** to review the agent deployment.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image107.png)

1. Copy the **Published URL** and paste it into Notepad for use in the next task.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image108.png)

1. Save the **Workspace ID** and **AISkills ID(Artifact ID)** in **Notepad** for later use.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image109.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image110.png)

1. Test the agent by entering the following prompt in the chat pane, and verify that the agent returns a response identifying products with a higher risk of stock depletion based on recent order activity.

    +++Predict which products may run out of stock soon.+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image111.png)


### Task 11: Create Foundry agent that unifies all IQ’s data

1. Open a browser go to +++https://portal.azure.com/+++ and sign in with your cloud slice account below.

1. Select your **AgenticAI** Resource group.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image112.png)

1. Select **Foundry project**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image113.png)

1. On the Overview pane, click on **Go to Foundry portal**. This will navigate you to the Microsoft Foundry portal.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image114.png)

    >[!Note] In the Microsoft Foundry portal, if prompted to select the project, select your recently created project from the list.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image115.png)

1. Select **Build** to proceed

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image116.png)

1. In the **Agents** section, locate and select the newly created agent (for example, **IQAgent**) from the list.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image117.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image118.png)

1. In the **Instructions** section, enter the following data to define the agent’s behavior. +++You are Contoso’s Resolution Agent for customer shipment and delivery issues. Your job is to: 1. Review customer and internal emails to understand the issue and urgency. 2. Use the Fabric Data Agent to validate customer, order, inventory, shipment, and support facts. 3. Use Foundry IQ to apply Contoso’s internal policies, SLA guidance, escalation criteria, and communication standards. 4. Recommend the best next action based on both data and policy. 5. Draft clear, professional customer-facing or internal responses when requested. Always: - Validate facts using available business data before making a recommendation. - Use policy documents when deciding replacement, refund, escalation, or SLA handling. - Distinguish between confirmed facts, likely causes, and recommended actions. - If inventory is available and policy supports replacement, prioritize fast resolution for Premium customers.+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image119.png)

1. Click **Save.**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image120.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image121.png)

1. In the **Knowledge** section, select **Add**, then choose **Connect to Foundry IQ** to link the agent with the data source.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image122.png)

1. In the **Connect to Foundry IQ** window, select **Connect to an AI Search resource** to configure the connection.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image123.png)

1. Select the **Foundry IQ resource** as **searchleaves2306402 (1)** from the drop-down, ensure **API Key** **(2)** is chosen as the authentication type, and then click **Connect** **(3)** to establish the connection with the Foundry IQ knowledge base.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image124.png)

1. Click **Create a knowledge base** and keep the name default and select model **GPT 5** in chat completions model and scroll down.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image125.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image126.png)

1. Click on **Add Sources** and select **Azure Blob storage** from the list

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image127.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image128.png)

    1. In the Choose a knowledge type window, first select the **Storage account** and **Container name** that were created in the previous steps. Then select Chat completions model as gpt-5 and click on **Create**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image129.png)

1. After configuring the knowledge base details make sure it is in **active** status (wait for 5 minutes or refresh) and select **Save knowledge base** to create and save it.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image130.png)

    >[!Note] If the status is not displayed as “Active”, refresh the page once and verify the status again.

1. Select **Use in an agent**, then choose the created agent (for example, **IQAgent**) to associate the knowledge base with it

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image131.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image132.png)

1. In the **Tools** section, select **Add**, then choose **Browse all tools** to view and configure additional tools for the agent.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image133.png)

1. In the **Catalog** tab, search for **Work IQ**, select **Work IQ Mail**, and then click **Create** to add the tool to the agent.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image134.png)

1. In the **Connect the Work IQ Mail tool** window, review the default settings and select **Connect** to complete the configuration.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image135.png)

1. Verify that **Work IQ Mail** is connected successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image136.png)

1. In the **Tools** section, select **Add**, then choose **Browse all tools** to view and configure additional tools for the agent.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image137.png)

1. Search for **Fabric Data Agent** under the **Configured** tab, select the **Fabric Data Agent** tool, and then click **Add tool** to add it to the agent.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image138.png)

1. In the **Connect to Fabric Data Agent** window, enter the required **Workspace ID** and **Artifact ID**, then select **Connect** to complete the setup.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image139.png)

1. Verify that **Fabric Data Agent** and **Work IQ Mail** is connected successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image140.png)


### Task 12: Create Demo mail to agent

1. Enter the following URL in the new tab to navigate to the Outlook:

    +++https://outlook.office.com/+++

1. Login with the provided user credentials provided below:

    - Username - +++@lab.CloudPortalCredential(User1).Username+++
    - Password - +++@lab.CloudPortalCredential(User1).AccessToken+++


    1. In Outlook, select **New mail (1)** to create a new email.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image141.png)

1. Enter the following details to draft an email:

    - **To (1)**: +++odl_user_2306402@sandboxailabs1012.onmicrosoft.com+++


## Email 1:

Subject: Urgent: Missing and Damaged Devices in Order O5001

Hello Team,  
  
We received our order O5001 for 25 Contoso ProBook 14 laptops today.  
  
However, only 18 units were delivered, and out of those, 4 units appear to be physically damaged on arrival. We are onboarding a new office team this Friday, so this delay is creating a serious operational issue for us.
  
Please investigate and let us know how soon the missing and damaged units can be resolved.
  
Regards, Ritika Sharma IT Procurement Lead Apex Legal Solutions

## Email 2

Subject: Fwd: Urgent customer issue - Apex Legal / O5001

Team,  
  
Apex Legal is one of our premium enterprise customers. Please review this immediately.
  
They are onboarding a new office and cannot afford delays. If replacement inventory is available, we should prioritize expedited fulfillment.
  
Can someone confirm what happened with this shipment and draft a response for the customer today?
  
Thanks, Maya Account Manager

## Email 3

Subject: Shipment exception review for O5001

Initial shipment scan indicates carton count discrepancy for order O5001.
  
There may have been a warehouse packing issue involving 7 units not loaded into the outbound pallet. A separate damage note was also recorded during final-mile delivery for 4 units.
  
Pending final confirmation.

- Then click on **Send (4)** to mail the products detail for replacement
  to ODL User.


![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image142.png)

1. After sending the email, open the Inbox and verify that the recipient has received the message.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image143.png)

1. A chat panel will open where you can enter your prompts. The agent will now respond.

    Review the latest Apex Legal email and Summarize.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image144.png)

1. Select **Approve** to grant the required permissions and continue.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image145.png)

1. Select **Always Approve this tool**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image146.png)

1. A chat panel will open where you can enter your prompts. The agent will now respond

    +++Is this customer eligible for replacement based on our policy?+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image147.png)

1. A chat panel will open where you can enter your prompts. The agent will now respond.

    +++Should this issue be escalated?+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image148.png)

1. A chat panel will open where you can enter your prompts. The agent will now respond.

    +++Draft a customer response based on the issue and our communication standards.+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2004/media/image149.png)


### Summary

In this use case, you successfully built an end-to-end **AI-powered customer resolution system** by combining data, knowledge, and communication tools. The agent can intelligently analyze customer complaints, validate order and shipment details, apply organizational policies, and recommend the best course of action. By integrating Work IQ, Foundry IQ, and Fabric IQ, the solution demonstrates how organizations can move from reactive support processes to proactive, data-driven decision-making. This approach not only improves resolution time and accuracy but also enhances customer experience and operational productivity.
