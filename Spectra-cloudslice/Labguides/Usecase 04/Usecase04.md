# Usecase 04-Build a customer resolution agent grounded with Work IQ, Foundry IQ, and Fabric IQ

**Introduction**

This use case focuses on building an intelligent **customer resolution
agent** for Contoso Electronics by integrating multiple Microsoft AI
capabilities, including Azure AI Search, Microsoft Fabric, and Microsoft
Foundry.

The solution simulates a real-world operations and support environment
where customer issues such as shipment delays, refunds, and escalations
are handled using AI-driven insights. The agent leverages structured
data (orders, inventory, support tickets), unstructured data (emails),
and policy knowledge to provide accurate recommendations and automate
responses. This creates a unified Copilot-like experience that enhances
operational efficiency and customer satisfaction.

**Objectives**

The main objectives of this use case are:

- To create and configure an **Azure AI Search** service for indexing
  and retrieving enterprise documents.

- To set up a **storage account** and ingest policy and operational
  documents for knowledge grounding.

- To build a **Foundry Agent** that acts as a customer support and
  operations assistant.

- To create a **Microsoft Fabric workspace and lakehouse** for storing
  and managing business data such as customers, orders, and shipments.

- To design an **ontology model** that defines relationships between
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

## Generate Email samples

- Send email samples (**C:\LabFiles\LabFiles\Usecase 6\\**WorkIQ
  Labfiles) from mail id of your choice to your tenant id.

![](./media/image1.png)

## Task 1: Create an Azure AI Search resource

In this exercise, you will create an Azure AI Search resource from the
Azure portal. This will be used to search the documents using AI
capability.

**Azure AI Search** is a cloud-based service for searching within your
privately curated data. It uses a combination of Microsoft’s AI and
JSON-based indexes to provide fast, relevant search results.

1.  Open a browser and login to Azure portal at
    +++<https://portal.azure.com/+++> with your credentials.

    - Username - <+++@lab.CloudPortalCredential>(User1).Username+++

    - Password - <+++@lab.CloudPortalCredential>(User1).Password+++

From the Home page of the Azure portal, select **Microsoft Foundry** and
select **Microsoft Foundry** under Services.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image2.png)

2.  In the **AI Foundry page**, select **AI Search** under **Use with AI
    Foundry** from the left pane and then select **+ Create**.

![](./media/image3.png)

3.  Enter the below details and select **Review + create**.

    - Subscription – Select your **assigned subscription**

    - Resource group – Select your **assigned Resource
      group** (**ResourceGroup1**)

    - Storage account name –
      +++[**searchleaves@lab.LabInstance.Id**](mailto:searchleaves@lab.LabInstance.Id)+++

    - Location – Select @lab.CloudResourceGroup(ResourceGroup1).Location

![A screenshot of a search service AI-generated content may be
incorrect.](./media/image4.png)

4.  Once the validation passes, select **Create**.

![A screenshot of a search engine AI-generated content may be
incorrect.](./media/image5.png)

5.  The deployment takes around 10 minutes to complete. Select **Go to
    resource** once the search service is created.

![](./media/image6.png)

6.  From the **Overview** page, copy the **Url** value and save it in a
    notepad to be used in a future exercise.

![](./media/image7.png)

7.  Select **Keys** under **Settings** from the left pane. Copy
    the **Primary admin key** and save it in a notepad for using it in
    the upcoming exercises.

![](./media/image8.png)

8.  Select **Identity** under **Settings** from the left pane.

![](./media/image9.png)

9.  Toggle the Status to **On** under **System assigned** and then click
    on **Save**.

![](./media/image10.png)

10. Select **Yes** in the **Enable system assigned managed
    identity** confirmation dialog.

![](./media/image11.png)

## Task 2: Create a Storage account

1.  From the Azure portal Home page (+++<https://portal.azure.com/+++>),
    select **Storage accounts**.

![](./media/image12.png)

2.  Select **+ Create** to create a new Storage account.

![](./media/image13.png)

3.  Enter the below details, accept the default values in the other
    fields and click on **Review + create**.

    - Subscription – Select your **assigned subscription**

    - Resource group – Select your **assigned Resource
      group** (**ResourceGroup1**)

    - Storage account name –
      +++[**iqlab@lab.LabInstance.Id**](mailto:iqlab@lab.LabInstance.Id)+++

    - Region – Select @lab.CloudResourceGroup(ResourceGroup1).Location

    - Primary service – Select **Azure Blob Storage or Azure Data Lake
      Storage Gen 2**

![](./media/image14.png)

4.  Once the validation passes, click on **Create**.

![](./media/image15.png)

5.  Once the resource creation succeeds, click on **Go to resource**.

![](./media/image16.png)

![](./media/image17.png)

6.  Select **Containers** under **Data storage**. Select **+
    Container**, enter the name as +++**document**+++ and click
    on **Create** to create the container.

![](./media/image18.png)

![](./media/image19.png)

7.  Select the created container **document** to upload the leave policy
    document into it.

> ![](./media/image20.png)

8.  Click on **Upload** and then select **Browse for files**.

![](./media/image21.png)

9.  Select the **all
    documents** from **C:\Labfiles\LabFiles\Usecase4\Foundry** and then
    click on **Upload**.

> ![](./media/image22.png)
>
> ![](./media/image23.png)
>
> ![](./media/image24.png)

10. Navigate to the
    +++[**iqlab@lab.LabInstance.Id**](mailto:iqlab@lab.LabInstance.Id)+++
    Storage account (Select **Storageaccounts** from the **Home
    page** of the Azure portal and select  and select **Access Control
    (IAM)** from the left pane. Select **Add -\> Add role assignment**.

![](./media/image25.png)

11. Search for +++**Storage Blob Data Reader**+++, select it and click
    on **Next**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image26.png)

12. Click on **+Select members**, search for and select your **user
    name**, <+++@lab.CloudPortalCredential>(User1).Username+++ and then
    click on **Select**. This adds the Storage Blob Data Reader role to
    your user id.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image27.png)

13. Select **Managed identity** and then select **+ Select members**.
    Select **Search service** under **Managed identity** and select
    the **searchleaves** search service that gets listed.

![](./media/image28.png)

14. Select **Review + assign** in the next 2 screens.

![](./media/image29.png)

![](./media/image30.png)

![](./media/image31.png)

## Task 3: Create Foundry resource

In this task, you will create a Foundry resource which is required to
access the Microsoft Foundry.

1.  From the Home page of the Azure
    portal(+++[https://portal.azure.com+++](https://portal.azure.com+++/)),
    select **Foundry**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image32.png)

2.  Select **Foundry** from the left pane, and then select **Create** to
    create the Foundry resource.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image33.png)

3.  Enter the below details and select **Review + create**.

    - Name - <+++agentic-@lab.LabInstance.Id>+++

    - Default project name
      - <+++agentic-ai-project-@lab.LabInstance.Id>+++

![](./media/image34.png)

4.  Select **Create** once validated.

![](./media/image35.png)

5.  Ensure that the resource is created.

![](./media/image36.png)

6.  Open
    the [**agentic-ai-project-@lab.LabInstance.Id**](mailto:agentic-ai-project-@lab.LabInstance.Id) and
    select **Go to Foundry portal**.

![](./media/image37.png)

7.  Click **Go to Foundry portal** 

![](./media/image38.png)

8.  In the top navigation, select **Build**

![](./media/image39.png)

9.  Select **Create agent** to create a new agent.

> ![](./media/image40.png)

10. Enter a unique agent name (e.g., **IQAgent**) and click **Create**
    to create the new agent.

![](./media/image41.png)

![](./media/image42.png)

## Task 4 : Create a Fabric workspace

In this task, you create a Fabric workspace. The workspace contains all
the items needed for this lakehouse tutorial, which includes lakehouse,
dataflows, Data Factory pipelines, the notebooks, Power BI datasets, and
reports.

1.  Open your browser, navigate to the address bar, and type or paste
    the following URL: +++https://app.fabric.microsoft.com/+++
    then press the **Enter** button and sign in with your credentials

[TABLE]

2.  In the Workspaces pane, click on **+New workspace** tile

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image43.png)

3.  In the **Create a workspace** pane that appears on the right side,
    enter the following details, and click on the **Apply** button.

[TABLE]

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image44.png)

![](./media/image45.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image46.png)

## Task 5: Create a lakehouse

1.  Create a new lakehouse by clicking on the **+New item** button in
    the navigation bar.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image47.png)

2.  Filter by, and select, the **+++Lakehouse+++** tile.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image48.png)

3.  In the **New lakehouse** dialog box, enter **+++IQ_Lakehouse
    +++** in the **Name** field and **unselect** the lakehouses schemas.
    Click on the **Create** button and open the new lakehouse.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image49.png)
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image50.png)

4.  You will see a notification stating **Successfully created SQL
    endpoint**.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image51.png)

## Task 6: Ingest sample data

1.  In the **IQ_Lakehouse** page, navigate to **Get data in your
    lakehouse** section, and click on **Upload files as shown in the
    below image.**

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image52.png)

2.  On the Upload files tab, click on the folder under the Files

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image53.png)

3.  Browse to **C:\LabFiles\LabFiles\Usecase 6\Fabric** on your VM, then
    select  ** all** tables and click on **Open** button.

> ![](./media/image54.png)

4.  Then, click on the **Upload** button and close the **Upload
    files** dialog by selecting the **X** icon for the dialog.

> ![](./media/image55.png)
>
> ![](./media/image56.png)

5.  Click and select refresh on the **Files**. The file appear.

> ![](./media/image57.png)

6.  In the **Lakehouse** page, Under the Explorer pane select **Files**.
    Now, hover your mouse over the **Customer.csv** file. Click on the
    horizontal ellipses **(…)** beside **Customer.csv**. Navigate and
    click on **Load Table**, then select **New table**.

> ![](./media/image58.png)
>
> ![](./media/image59.png)

7.  In the **Load file to new table** dialog box, click on
    the **Load** button.

> ![](./media/image60.png)

8.  Now successfully created **Customer** table

> ![](./media/image61.png)

9.  Repeat Steps 7 through 9 to push the remaining file into the tables.

![](./media/image62.png)

![](./media/image63.png)

![](./media/image64.png)

![](./media/image65.png)

10. From the left navigation bar, select **Fabric IQ Ontology**.

> ![](./media/image66.png)

## Task 7: Create ontology (preview) item

1.  In your Fabric workspace, select **+ New item**. Search for and
    select the **Ontology (preview)** item.

> ![](./media/image67.png)

2.  Enter +++**NetworkOperationsOntology+++** for the **Name** of your
    ontology and select **Create**.

> ![](./media/image68.png)
>
> ** Tip:** Ontology names can include numbers, letters, and
> underscores. Don't use spaces or dashes.

3.  The ontology opens when it's ready.

> ![](./media/image69.png)
>
> Next, create entity types, data bindings, and relationships based on
> data from your lakehouse tables.

## Task 8: Create Entity Types and Data Bindings

> Entity types represent categories of objects in your business domain.
> For this schema, you will create two entity
> types: **Tickets** and **Inspections**.

1.  From the top ribbon or the center of the configuration canvas,
    select **Add entity type**.

> ![](./media/image70.png)

2.  Enter +++**Customer**+++ as the name and select **Add Entity
    Type**. 

> ![](./media/image71.png)

3.  The **Tickets** entity type appears on the configuration canvas and
    the **Entity type configuration** pane opens.

> ![](./media/image72.png)

4.  Switch to the **Bindings** tab and select **Add data to entity
    type**.

> ![](./media/image73.png)

5.  Choose your data source: a. Select your **Lakehouse** and
    select **Add**. 

> ![](./media/image74.png)

6.  Select the **Customers** table and select **Next**. 

> ![](./media/image75.png)

7.  Configure a **Static** data binding:

- For **Binding type**, keep the default **Static**.

- Under **Bind your properties**, the columns from the tickets table
  populate automatically:

- Select **Save**.

> ![](./media/image76.png)

8.  Back in the Entity type configuration pane, select **Add entity type
    key**. 

> ![](./media/image77.png)

9.  Select **customer_id** as the key property and select **Save**.

> ![](./media/image78.png)

10. Select **Add entity type** from the ribbon. 

> ![](./media/image79.png)

11. Enter **Order** as the name and select **Add Entity Type**. 

> ![](./media/image80.png)

12. Switch to the **Bindings** tab → **Add data to entity type**. 

![](./media/image81.png)

13. Choose your data source, select your **Lakehouse** and
    select **Add**. 

> ![](./media/image82.png)

14. Select the **orders** table and select **Next**.

> ![](./media/image83.png)

15. Configure a **Static** data binding with the following columns:

- Select **Save**.

![](./media/image84.png)

16. Select **Add entity type key** 

![](./media/image85.png)

17. Select **OrderID** as the key property and select **Save**.

![](./media/image86.png)

> ![](./media/image87.png)

18. Follow the same steps that you used for the **Store** entity type to
    create the entity types described in the following table. Each
    entity has a static data binding with the default columns from its
    source table.

[TABLE]

> ![](./media/image88.png)
>
> ![](./media/image89.png)
>
> ![](./media/image90.png)
>
> ![](./media/image91.png)
>
> ![](./media/image92.png)
>
> ![](./media/image93.png)
>
> ![](./media/image94.png)

![](./media/image95.png)

## Task 9: Create relationship types

Next, create relationship types between the entity types to represent
contextual connections in your data.

1.  Select **Add relationship** from the menu ribbon.

![](./media/image96.png)

2.  Enter the following relationship type details and select **Add
    relationship type**.

    - **Relationship type name**: +++Places +++

    - **Source entity type**: Customer

    - **Target entity type**: Order

![](./media/image97.png)

3.  The **Relationship configuration** pane opens, where you can
    configure additional information. Enter the following details (some
    fields become visible based on other selections) and
    select **Create**.

    1.  **Source data**: Select your tutorial workspace, the **Fabric IQ
        Ontology_Lakehouse** lakehouse, and the **Customers** table.

![](./media/image98.png)

![](./media/image99.png)

Now the first relationship is created, and bound to data in your source
table. Continue to the next section to create another relationship type.

**Products soldIn SaleEvent**

4.  Follow the same steps that you used for the first relationship type
    to create the relationship type described in the following table.

[TABLE]

> ![](./media/image100.png)
>
> ![](./media/image101.png)
>
> ![](./media/image102.png)
>
> ![](./media/image103.png)
>
> ![](./media/image104.png)
>
> ![](./media/image105.png)
>
> ![](./media/image106.png)
>
> ![](./media/image107.png)
>
> ![](./media/image108.png)
>
> ![](./media/image109.png)
>
> ![](./media/image110.png)
>
> ![](./media/image111.png)
>
> ![](./media/image112.png)
>
> ![](./media/image113.png)
>
> ![](./media/image114.png)
>
> ![](./media/image115.png)

## Task 10: Create data agent with ontology (preview) source

Follow these steps to create a new data agent that connects to your
ontology (preview) item.

1.  Now, click on **Fabric IQ OntologyXX** on the left-sided navigation
    pane.

![](./media/image116.png)

2.  In the **Fabric** home page, select **+New item.** In the Filter by
    item type search box, enter +++**data agent**+++ and select the Data
    agent

> ![](./media/image117.png)

3.  Enter **+++**IQ_Agent**+++** as the Data agent name and
    select **Create**.

> ![](./media/image118.png)

4.  In **FabricDataAgent** page, select **Add a data source**

> ![](./media/image119.png)

5.  In the OneLake catalog tab, select the **NetworkOperationsOntology**
    Ontology and select **Add.**

![](./media/image120.png)

![](./media/image121.png)

19. Select **Agent instructions** to configure and customize the
    behavior of the agent.

![](./media/image122.png)

20. Enter the following data into the **Instructions** section, then
    select **Publish**.

> You are a customer operations and order resolution analytics agent.
>
> Your purpose is to help answer business questions related to:
>
> - customer orders
>
> - shipment issues
>
> - support escalations
>
> - refund or replacement claims
>
> - fulfillment delays
>
> - product availability
>
> - account history and trends
>
> Use business-friendly language and provide concise but useful answers.
>
> Interpret the data using these business concepts:
>
> - A customer can place many orders.
>
> - An order can contain multiple products.
>
> - An order can have shipment incidents, tracking events, support
> tickets, and refund claims.
>
> - A customer can also have account notes that provide relationship or
> operational context.
>
> - Inventory reflects current stock availability by SKU and warehouse.
>
> Use these tables/concepts for the following question types:
>
> 1. Customer and order history
>
> - Use Customers, Orders, OrderItems, and AccountNotes.
>
> - When asked about a customer’s background, summarize recent orders,
> important account notes, and notable support or shipment history.
>
> 2. Shipment and delivery issues
>
> - Use Orders, ShipmentIncidents, ShipmentTracking, and SupportTickets.
>
> - When asked about delays, damaged shipments, shortages, or delivery
> problems, prioritize these sources.
>
> 3. Refunds and replacements
>
> - Use RefundClaims, ShipmentIncidents, SupportTickets, and Orders.
>
> - When asked whether a refund or replacement is appropriate, look for
> shipment issues, customer complaints, and prior claim patterns.
>
> 4. Product and stock availability
>
> - Use Inventory and OrderItems.
>
> - When asked whether a replacement can be fulfilled, check whether the
> requested SKU is available in stock.
>
> 5. Trend and historical analysis
>
> - Use Orders, ShipmentIncidents, RefundClaims, SupportTickets, and
> ShipmentTracking.
>
> - When asked for trends, summarize patterns by month, issue type,
> customer, or product where appropriate.
>
> Important interpretation rules:
>
> - “Issue”, “problem”, or “complaint” may refer to shipment incidents,
> support tickets, or refund claims.
>
> - “Replacement” and “reshipment” should be treated as operational
> recovery actions.
>
> - “Escalation” usually refers to urgent or unresolved support or
> delivery issues.
>
> - “High-risk customer” may indicate repeated shipment issues, open
> tickets, unresolved claims, or negative account notes.
>
> - “Historical trend” means analysis over time, usually by month unless
> otherwise specified.
>
> Response guidance:
>
> - Prefer summaries over raw data dumps.
>
> - If the user asks for trends, provide a short interpretation in
> addition to the numbers.
>
> - If there is insufficient data, clearly say so.
>
> - If multiple records exist, prioritize the most recent and most
> severe items.
>
> - If asked for a recommendation, provide a business-oriented
> recommendation based on the available evidence.
>
> Support group by in GQL

![](./media/image123.png)

> ![](./media/image124.png)

21. After publishing, verify the success message and select **View
    publishing details** to review the agent deployment.

> ![](./media/image125.png)

22. Copy the **Published URL** and paste it into Notepad for use in the
    next task.

> ![](./media/image126.png)

23. Save the **Workspace ID** and **AISkills ID** in **Notepad** for
    later use

![](./media/image127.png)

![](./media/image128.png)

![](./media/image129.png)

## Task 11: Create Foundry agent that unifies all IQ’s data

1.  Open a browser go to
    +++[https://portal.azure.com+++](https://portal.azure.com+++/) and
    sign in with your cloud slice account below.

2.  Select your **Resource group**

![](./media/image130.png)

3.  Select **Foundry project**

> ![](./media/image131.png)

4.  On the Overview pane, click on **Go to Foundry portal**. This will
    navigate you to the Microsoft Foundry portal.

![](./media/image132.png)

5.  Select **Build** to proceed

![](./media/image133.png)

6.  In the **Agents** section, locate and select the newly created agent
    (for example, **IQAgent**) from the list.

![](./media/image134.png)

![](./media/image135.png)

7.  In the **Instructions** section, enter the following data to define
    the agent’s behavior.

> You are Contoso’s Resolution Agent for customer shipment and delivery
> issues.
>
> Your job is to:
>
> 1. Review customer and internal emails to understand the issue and
> urgency.
>
> 2. Use the Fabric Data Agent to validate customer, order, inventory,
> shipment, and support facts.
>
> 3. Use Foundry IQ to apply Contoso’s internal policies, SLA guidance,
> escalation criteria, and communication standards.
>
> 4. Recommend the best next action based on both data and policy.
>
> 5. Draft clear, professional customer-facing or internal responses
> when requested.
>
> Always:
>
> - Validate facts using available business data before making a
> recommendation.
>
> - Use policy documents when deciding replacement, refund, escalation,
> or SLA handling.
>
> - Distinguish between confirmed facts, likely causes, and recommended
> actions.
>
> - If inventory is available and policy supports replacement,
> prioritize fast resolution for Premium customers.

![](./media/image136.png)

8.  Click **Save**

![](./media/image137.png)

![](./media/image138.png)

9.  In the **Knowledge** section, select **Add**, then choose **Connect
    to Foundry IQ** to link the agent with the data source.

> ![](./media/image139.png)

10. In the **Connect to Foundry IQ** window, select **Connect to an AI
    Search resource** to configure the connection.

> ![](./media/image140.png)

11. In the **Choose a knowledge type** window, select **Azure Blob
    Storage**, then click **Connect** to proceed.

![](./media/image141.png)

12. In the **Choose a knowledge type** window, select Chat completions
    model as gpt-4.1 and click on **create**

> ![](./media/image142.png)

13. After configuring the knowledge base details, select **Save
    knowledge base** to create and save it.

![](./media/image143.png)

![](./media/image144.png)

![](./media/image145.png)

14. Verify that the knowledge source is added successfully and its
    status is **Active**.

![](./media/image146.png)

11. Select **Use in an agent**, then choose the created agent (for
    example, **IQAgent**) to associate the knowledge base with it

![](./media/image147.png)

![](./media/image148.png)

12. In the **Tools** section, select **Add**, then choose **Browse all
    tools** to view and configure additional tools for the agent.

![](./media/image149.png)

13. In the **Catalog** tab, search for **Work IQ**, select **Work IQ
    Mail**, and then click **Create** to add the tool to the agent.

![](./media/image150.png)

14. In the **Connect the Work IQ Mail tool** window, review the default
    settings and select **Connect** to complete the configuration.

![](./media/image151.png)

15. Verify that **Work IQ Mail** is connected successfully.

![](./media/image152.png)

16. In the **Tools** section, select **Add**, then choose **Browse all
    tools** to view and configure additional tools for the agent.

![](./media/image153.png)

17. Select **Fabric Data Agent**, and then click **Create** to add the
    tool to the agent.

![](./media/image154.png)

18. In the **Connect to Fabric Data Agent** window, enter the required
    **Workspace ID** and **Artifact ID**, then select **Connect** to
    complete the setup.

![](./media/image155.png)

19. Verify that **Fabric Data Agent** and **Work IQ Mail** is connected
    successfully.

![](./media/image156.png)

20. A chat panel will open where you can enter your prompts. The agent
    will now respond.

> +++Review the latest Apex Legal email and tell me what happened.+++

![](./media/image157.png)

21. Select **Approve** to grant the required permissions and continue.

![](./media/image158.png)

22. Select **Always Approve this tool**

![](./media/image159.png)

23. A chat panel will open where you can enter your prompts. The agent
    will now respond

> +++Is this customer eligible for replacement based on our policy?+++
>
> ![](./media/image160.png)
>
> ![](./media/image161.png)

25. A chat panel will open where you can enter your prompts. The agent
    will now respond

> +++Do we have enough stock to resolve this today?+++
>
> ![](./media/image162.png)
>
> ![](./media/image163.png)

26. A chat panel will open where you can enter your prompts. The agent
    will now respond

> +++Should this issue be escalated?+++

![](./media/image164.png)

![](./media/image165.png)

27. A chat panel will open where you can enter your prompts. The agent
    will now respond

+++Draft a customer response based on the issue and our communication
standards.+++

![](./media/image166.png)

28. A chat panel will open where you can enter your prompts. The agent
    will now respond

> +++ What is the best operational resolution for order O5001?+++
>
> ![](./media/image167.png)

![](./media/image168.png)

> **Summary**
>
> In this use case, you successfully built an end-to-end **AI-powered
> customer resolution system** by combining data, knowledge, and
> communication tools. The agent can intelligently analyze customer
> complaints, validate order and shipment details, apply organizational
> policies, and recommend the best course of action.
>
> By integrating Work IQ, Foundry IQ, and Fabric IQ, the solution
> demonstrates how organizations can move from reactive support
> processes to proactive, data-driven decision-making. This approach not
> only improves resolution time and accuracy but also enhances customer
> experience and operational productivity.
