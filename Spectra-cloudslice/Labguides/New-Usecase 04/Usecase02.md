# Usecase 02: Build a customer resolution agent grounded with Work IQ, Foundry IQ, and Fabric IQ

**Scenario**

**Contoso Electronics** sells laptops and devices to enterprise customers. When something goes wrong with an order — a short shipment, damaged units, a delayed delivery or a refund request — the support and account teams have to piece together the answer from several places: the customer's emails, order and shipment data in different systems, and internal policies for replacements, SLAs and escalations. This slows down responses, especially for premium customers who expect fast resolution.

Contoso wants a single **customer resolution agent** that can read the customer's emails, check the facts in the business data, apply the company's policies, recommend the best next action, and draft a professional response.

As an AI engineer at Contoso, you will build this agent in **Microsoft Foundry** and ground it with three sources of knowledge:

- **Work IQ** – the customer and internal emails in Outlook.
- **Foundry IQ** – Contoso's policy documents, indexed with Azure AI Search.
- **Fabric IQ** – an ontology in Microsoft Fabric that models customers, orders, products, shipments, refund claims and support tickets.

**Introduction**

In this use case, you build an intelligent **customer resolution agent** for Contoso Electronics by integrating Azure AI Search, Microsoft Fabric and Microsoft Foundry. The solution simulates a real-world operations and support environment where customer issues such as shipment delays, refunds and escalations are handled using AI-driven insights. The agent uses structured data (orders, inventory, support tickets), unstructured data (emails) and policy knowledge to provide accurate recommendations and automate responses, creating a unified Copilot-like experience that improves operational efficiency and customer satisfaction.

**Resources created in this lab**

| **Resource** | **Name** | **Role in the lab** |
|----|----|----|
| Azure AI Search | searchleaves\<lab instance ID\> | Indexes the policy documents for Foundry IQ |
| Storage account | storage\<lab instance ID\> | Stores the policy documents in the **document** container |
| Foundry resource and project | agentic-\<lab instance ID\> / agentic-ai-project-\<lab instance ID\> | Hosts the **IQAgent** customer resolution agent |
| Fabric workspace | Fabric IQ Ontology-\<lab instance ID\> | Contains the lakehouse and the ontology |
| Lakehouse | IQ_Lakehouse | Stores customers, orders, inventory, shipments, refund claims and support tickets |
| Ontology (preview) | NetworkOperationsOntology | Models the business entities and their relationships (Fabric IQ) |

**Objectives**:

- Create and configure an **Azure AI Search** service for indexing and retrieving enterprise documents.

- Set up a **storage account** and upload policy and operational documents for knowledge grounding.

- Create a **Foundry agent** that acts as a customer support and operations assistant.

- Create a **Microsoft Fabric workspace and lakehouse** to store business data such as customers, orders and shipments.

- Design an **ontology** that defines relationships between entities such as customers, orders, support tickets and refund claims.

- Integrate **Work IQ (email)**, **Foundry IQ (policies)** and **Fabric IQ (data)** into a single agent.

- Use the agent to analyze customer issues, validate data across systems, apply business policies, recommend resolutions and generate professional responses.

## Exercise 1: Prepare the Azure resources

In this exercise, you create the Azure AI Search service, the storage account with the policy documents, and the Foundry resource and agent.

### Task 1: Create an Azure AI Search resource

**Azure AI Search** is a cloud-based service for searching within your privately curated data. It uses a combination of Microsoft's AI and JSON-based indexes to provide fast, relevant search results. In this task, you create the search service that Foundry IQ uses to search the policy documents.

1.  Open your browser, navigate to the address bar, and type or paste the following URL: +++https://portal.azure.com/+++ then press the **Enter** button. Sign in with the following credentials.

| **Username** | **+++@lab.CloudPortalCredential(User1).Username+++** |
|----|----|
| **Temporary Access Pass** | **+++@lab.CloudPortalCredential(User1).AccessToken+++** |

![](./media/image1.png)

![](./media/image2.png)

2.  When prompted with the **Stay signed in?** dialog, select **No** to continue.

![](./media/image3.png)

3.  From the Home page of the Azure portal, search for +++Microsoft Foundry+++ and select **Microsoft Foundry** under **Services**.

![](./media/image4.png)

4.  On the **Microsoft Foundry** page, select **AI Search (1)** under **Use with Foundry** in the left pane, and then select **+ Create (2)**.

![](./media/image5.png)

5.  Enter the following details and select **Review + create (4)**.

| **Subscription** | Select your assigned subscription |
|----|----|
| **Resource group** | **AgenticAI (1)** |
| **Service name** | +++searchleaves@lab.LabInstance.Id+++ **(2)** |
| **Location** | **Central US (3)** |

![](./media/image6.png)

6.  Once the validation passes, select **Create**.

![](./media/image7.png)

7.  The deployment takes around 10 minutes to complete. Select **Go to resource** once the search service is created.

![](./media/image8.png)

8.  On the **Overview** page, copy the **Url** value and save it in Notepad for a later exercise.

![](./media/image9.png)

9.  Select **Keys (1)** under **Security + networking** in the left pane. Copy the **Primary admin key (2)** and save it in Notepad for a later exercise.

![](./media/image10.png)

10. Select **Identity (1)** under **Security + networking** in the left pane.

11. Under **System assigned**, toggle the **Status** to **On (2)**, and then click on **Save (3)**.

![](./media/image11.png)

12. Select **Yes** in the **Enable system assigned managed identity** confirmation dialog.

![](./media/image12.png)

### Task 2: Create a storage account and upload the policy documents

1.  In the Azure portal search bar, search for +++Storage accounts+++ **(1)** and select **Storage accounts (2)**.

![](./media/image13.png)

2.  Select **+ Create** to create a new storage account.

![](./media/image14.png)

3.  Enter the following details, accept the default values in the other fields, and click on **Review + create**.

| **Subscription** | Select your assigned subscription |
|----|----|
| **Resource group** | **AgenticAI (1)** |
| **Storage account name** | +++storage@lab.LabInstance.Id+++ **(2)** |
| **Region** | **Central US (3)** |
| **Primary service** | **Azure Blob Storage or Azure Data Lake Storage (4)** |

![](./media/image15.png)

4.  Once the validation passes, click on **Create**.

![](./media/image16.png)

5.  Once the resource is created, click on **Go to resource**.

![](./media/image17.png)

6.  Expand **Data storage (1)**, select **Containers (2)**, and then click on **+ Add container (3)**.

![](./media/image18.png)

7.  In the **New container** pane, enter +++document+++ **(1)** as the name and click on **Create (2)**.

![](./media/image19.png)

8.  Select the **document** container to upload the policy documents into it.

![](./media/image20.png)

9.  Click on **Upload (1)** and then select **Browse for files (2)**.

![](./media/image21.png)

10. Browse to **C:\Labfiles\lab file\Usecase4\Foundry**, select **all the documents**, and then click on **Open** and **Upload**.

![](./media/image22.png)

![](./media/image23.png)

![](./media/image24.png)

11. Navigate back to the **storage@lab.LabInstance.Id** storage account. Select **Access control (IAM)** in the left pane, and then select **+ Add \> Add role assignment**.

![](./media/image25.png)

12. Search for +++Storage Blob Data Reader+++ **(1)**, select it **(2)**, and click on **Next (3)**.

![](./media/image26.png)

13. Click on **+ Select members** under **User, group, or service principal**, search for and select **+++@lab.CloudPortalCredential(User1).Username+++**, and then click on **Select**. Select **Review + assign** twice. This assigns the **Storage Blob Data Reader** role to your user account.

14. Repeat steps 11 and 12 to start a second **Storage Blob Data Reader** role assignment, this time for the search service.

15. Select **Managed identity (1)**, and then select **+ Select members (2)**. Under **Managed identity**, select **Search service (3)**, select the **searchleaves@lab.LabInstance.Id (4)** search service, and then click on **Select (5)**.

16. Select **Review + assign (6)**.

![](./media/image27.png)

17. Click on **Review + assign** again to assign the role.

![](./media/image28.png)

### Task 3: Create a Foundry resource and agent

In this task, you create the Foundry resource and project, and then create the **IQAgent** agent that you configure later in the lab.

1.  From the Home page of the Azure portal (+++https://portal.azure.com+++), select **Foundry**.

![](./media/image29.png)

2.  Select **Foundry** in the left pane, and then select **+ Create** to create the Foundry resource.

![](./media/image30.png)

3.  Enter the following details and select **Review + create (5)**.

| **Resource group** | **AgenticAI (1)** |
|----|----|
| **Name** | +++agentic-@lab.LabInstance.Id+++ **(2)** |
| **Region** | Keep the default region |
| **Default project name** | +++agentic-ai-project-@lab.LabInstance.Id+++ **(4)** |

![](./media/image31.png)

4.  Select **Create** once validated.

![](./media/image32.png)

5.  Make sure that the resource is created.

![](./media/image33.png)

6.  Navigate to the **AgenticAI** resource group.

![](./media/image34.png)

7.  Open the **agentic-ai-project-@lab.LabInstance.Id** project.

![](./media/image35.png)

8.  Click on **Go to Foundry portal**.

![](./media/image36.png)

9.  In the top navigation, select **Build**.

![](./media/image37.png)

**Note:** If you get permission errors, assign yourself the **Foundry User** role:

- Navigate to the **AgenticAI** resource group.

- Under **Access control (IAM) (1)**, select **Add role assignment (3)** from the **+ Add** drop-down.

![](./media/image38.png)

- Search for +++Foundry User+++, select it from the list **(2)**, and click on **Next (3)**.

- Click on **+ Select members**, search for **+++@lab.CloudPortalCredential(User1).Username+++**, select your user, click on **Select**, and then click on **Review + assign** twice.

![](./media/image39.png)

10. Navigate to the **Agents** page **(1)**, click on **New agent (2)**, and then select **Build an agent (3)** to create a new agent with the visual builder.

![](./media/image40.png)

11. Enter +++IQAgent+++ **(1)** as the agent name, and then click on **Create and open playground (2)**.

![](./media/image41.png)

![](./media/image42.png)

## Exercise 2: Build the Fabric IQ ontology

In this exercise, you create a Fabric workspace and lakehouse, load Contoso's business data, and build an ontology that models customers, products, orders, shipments, refund claims and support tickets.

### Task 1: Create a Fabric workspace

In this task, you create a Fabric workspace that contains all the Fabric items for this lab.

1.  Open your browser, navigate to the address bar, and type or paste the following URL: +++https://app.fabric.microsoft.com/+++ then press the **Enter** button and sign in with the following credentials.

| **Username** | **+++@lab.CloudPortalCredential(User1).Username+++** |
|----|----|
| **Password** | **+++@lab.CloudPortalCredential(User1).Password+++** |

![](./media/image43.png)

2.  If Power BI opens by default, follow these steps; otherwise, skip this step:

- Click on **Power BI**.

![](./media/image44.png)

- Select **Fabric** from the options.

![](./media/image45.png)

3.  In the **Workspaces** pane, click on the **+ New workspace** tile.

![](./media/image46.png)

4.  In the **Create a workspace** pane that appears on the right side, enter +++Fabric IQ Ontology-@lab.LabInstance.Id+++ **(1)** as the name, and expand the **Advanced (2)** section.

![](./media/image47.png)

5.  Select **Fabric (1)** as the workspace type, choose the capacity assigned to your lab **(2)**, make sure **Small semantic model storage format (3)** is selected, and then click on **Apply (4)** to create the workspace.

![](./media/image48.png)

### Task 2: Create a lakehouse

1.  Create a new lakehouse by clicking on the **+ New item** button in the navigation bar.

![](./media/image49.png)

2.  Filter by +++Lakehouse+++ and select the **Lakehouse** tile under **Store data**.

![](./media/image50.png)

3.  In the **New lakehouse** dialog box, enter +++IQ_Lakehouse+++ **(1)** in the **Name** field and **unselect (2)** **Lakehouse schemas**. Click on the **Create (3)** button and open the new lakehouse.

![](./media/image51.png)

4.  You will see a notification stating **Successfully created SQL endpoint**.

![](./media/image52.png)

### Task 3: Ingest the sample data

1.  On the **IQ_Lakehouse** page, navigate to the **Get data in your lakehouse** section, and click on **Upload files**.

![](./media/image53.png)

2.  On the **Upload files** tab, click on the folder icon under **Files**.

![](./media/image54.png)

3.  Browse to **C:\LabFiles\lab file\Usecase4\Fabric (1)** on your VM, select **all the CSV files (2)**, and click on the **Open (3)** button.

![](./media/image55.png)

4.  Click on the **Upload** button, and then close the **Upload files** dialog by selecting the **X** icon.

![](./media/image56.png)

![](./media/image57.png)

5.  Select **Files** and click on **Refresh**. The files appear.

![](./media/image58.png)

6.  In the **Explorer** pane, select **Files**. Hover your mouse over the **Customers.csv** file, click on the horizontal ellipses **(…) (1)** beside it, click on **Load to Tables**, and then select **New table**.

![](./media/image59.png)

![](./media/image60.png)

7.  In the **Load file to new table** dialog box, enter +++customers+++ as the table name, and then click on the **Load** button.

![](./media/image61.png)

8.  The **customers** table is now successfully created.

![](./media/image62.png)

9.  Repeat steps 6 through 8 to load the remaining files into tables. Keep the default table names: **inventory**, **orderitems**, **orders**, **refundclaims**, **shipmenttracking** and **supporttickets**.

![](./media/image63.png)

**Note:** If you encounter Fabric capacity issues during the lab, navigate to **Fabric Capacity** in the Azure portal, pause the capacity for approximately **5 minutes**, and then resume it. Once the capacity is running successfully, continue with the remaining lab steps.

10. From the left navigation bar, select the **Fabric IQ Ontology-@lab.LabInstance.Id** workspace.

![](./media/image64.png)

![](./media/image65.png)

### Task 4: Create an ontology (preview) item

1.  In your Fabric workspace, select **+ New item**. Search for and select the **Ontology (preview)** item.

![](./media/image66.png)

**Note:** In some cases, the **Ontology (preview)** item may not appear immediately in the **+ New item** search results. If this happens, sign out of the Fabric portal, sign in again, and retry the search.

2.  Enter +++NetworkOperationsOntology+++ **(1)** as the ontology name, verify the workspace location, and then click on **Create (2)**.

![](./media/image67.png)

**Note:** Ontology names can include numbers, letters and underscores. Don't use spaces or dashes.

3.  The ontology opens when it's ready.

![](./media/image68.png)

**Note:** If you face issues loading the tables, restart the Fabric capacity from the Azure portal.

Next, you create entity types, data bindings and relationships based on the data in your lakehouse tables.

### Task 5: Create the entity types

In this task, you create seven entity types and bind each one to a lakehouse table.

| **Entity type** | **Source table** | **Entity type key** |
|----|----|----|
| Customer | customers | CustomerID |
| Products | inventory | ProductID |
| SalesOrder | orders | OrderID |
| OrderItem | orderitems | OrderItemID |
| Shipment | shipmenttracking | TrackingID |
| RefundClaim | refundclaims | ClaimID |
| SupportTicket | supporttickets | TicketID |

**Note:** **PRODUCT** and **ORDER** are reserved words in GQL, the graph query language used to query the ontology. Using a plural (**Products**) or a prefix (**SalesOrder**) avoids query errors later.

**Customer**

1.  Select **Add entity type** from the top ribbon (or the center of the canvas). Enter +++Customer+++ and select **Add Entity Type**.

![](./media/image69.png)

![](./media/image70.png)

2.  On the canvas, select **...** next to **Customer**, and then select **Bind data**.

![](./media/image71.png)

3.  Under **Add a data source**, select **Add**. In the **OneLake catalog**, expand **IQ_Lakehouse**, select the **customers** table, and then select **Select table**.

![](./media/image72.png)

![](./media/image73.png)

4.  Select **Entity type properties**, review the properties that are populated from the table columns, and select **Create**. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image74.png)

![](./media/image75.png)

![](./media/image76.png)

5.  On the **Configure** page, next to **Entity type key**, select **Define entity type key**.

![](./media/image77.png)

6.  In the **Add or edit key** dialog, select **CustomerID**, and then select **Save**.

![](./media/image78.png)

**Note:** The screenshot shows **customer_id** from an earlier version of the data file. Select **CustomerID**.

7.  Verify that the **Entity type key** shows the key, and then select **Home** to return to the configuration canvas.

![](./media/image79.png)

**Products**

8.  On the **Home** tab, select **Add entity type**.

![](./media/image80.png)

9.  Enter +++Products+++ and select **Add Entity Type**.

![](./media/image81.png)

10. On the canvas, select **...** next to **Products**, and then select **Bind data**.

![](./media/image82.png)

11. Under **Add a data source**, select **Add**.

![](./media/image83.png)

12. In the **OneLake catalog**, expand **IQ_Lakehouse**, select the **inventory** table, and then select **Select table**.

![](./media/image84.png)

13. Select **Entity type properties**.

![](./media/image85.png)

14. Review the property mappings: **InventoryID**, **ProductID**, **ProductName**, **Category**, **StockQuantity**, **WarehouseLocation** and **LastUpdated**. Keep the defaults.

![](./media/image86.png)

15. Select **Create**.

![](./media/image87.png)

16. If the **Save** button is shown, select **Save**. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image88.png)

![](./media/image89.png)

17. On the **Configure** page, select **Define entity type key**.

![](./media/image90.png)

18. Select **ProductID**, and then select **Save**.

![](./media/image91.png)

19. Verify that the key icon appears next to **ProductID**, and then select **Home**.

![](./media/image92.png)

**Note:** If you see a **Timeseries data** section on the binding page, ignore it. All tables in this lab are static data.

**SalesOrder**

20. On the **Home** tab, select **Add entity type**.

![](./media/image93.png)

21. Enter +++SalesOrder+++ and select **Add Entity Type**.

![](./media/image94.png)

22. Select **...** next to **SalesOrder**, and then select **Bind data**.

![](./media/image95.png)

23. Select **Add**.

![](./media/image96.png)

24. Expand **IQ_Lakehouse**, select the **orders** table, and select **Select table**.

![](./media/image97.png)

25. Select **Entity type properties**, review the properties (**OrderID**, **CustomerID**, **OrderDate**, **OrderStatus**, **TotalAmount**), and select **Create**.

![](./media/image98.png)

26. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image99.png)

27. Select **Define entity type key**, select **OrderID**, and select **Save**.

![](./media/image100.png)

28. Verify the key, and then select **Home**.

![](./media/image101.png)

**OrderItem**

29. Select **Add entity type**, enter +++OrderItem+++, and select **Add Entity Type**.

![](./media/image102.png)

30. Select **...** next to **OrderItem**, and then select **Bind data**.

![](./media/image103.png)

31. Select **Add**.

![](./media/image104.png)

32. Expand **IQ_Lakehouse**, select the **orderitems** table, and select **Select table**.

![](./media/image105.png)

33. Select **Entity type properties**, review the properties (**OrderItemID**, **OrderID**, **ProductID**, **Quantity**, **UnitPrice**), and select **Create**.

![](./media/image106.png)

34. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image107.png)

35. Select **Define entity type key**, select **OrderItemID**, and select **Save**.

![](./media/image108.png)

36. Select **Home**.

![](./media/image109.png)

**Shipment**

37. Select **Add entity type**, enter +++Shipment+++, and select **Add Entity Type**.

![](./media/image110.png)

38. Select **...** next to **Shipment**, and then select **Bind data**.

![](./media/image111.png)

39. Select **Add**.

![](./media/image112.png)

40. Expand **IQ_Lakehouse**, select the **shipmenttracking** table, and select **Select table**.

![](./media/image113.png)

41. Select **Entity type properties**, review the properties (**TrackingID**, **OrderID**, **ShipmentStatus**, **ShippedDate**, **DeliveryDate**), and select **Create**.

![](./media/image114.png)

42. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image115.png)

43. Select **Define entity type key**, select **TrackingID**, and select **Save**.

![](./media/image116.png)

**RefundClaim**

44. Select **Home (1)**, select **Add entity type (2)**, enter +++RefundClaim+++ **(3)**, and select **Add Entity Type (4)**.

![](./media/image117.png)

45. Select **...** next to **RefundClaim**, and then select **Bind data**.

![](./media/image118.png)

46. Select **Add**.

![](./media/image119.png)

47. Expand **IQ_Lakehouse**, select the **refundclaims** table, and select **Select table**.

![](./media/image120.png)

48. Select **Entity type properties**, review the properties (**ClaimID**, **OrderID**, **Reason**, **ClaimStatus**, **ClaimDate**), and select **Create**. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image121.png)

49. Select **Define entity type key**, select **ClaimID**, and select **Save**.

![](./media/image122.png)

**SupportTicket**

50. Select **Home**, select **Add entity type**, enter +++SupportTicket+++, and select **Add Entity Type**.

![](./media/image123.png)

51. Select **...** next to **SupportTicket**, and then select **Bind data**.

![](./media/image124.png)

52. Select **Add**.

![](./media/image125.png)

53. Expand **IQ_Lakehouse**, select the **supporttickets** table, and select **Select table**.

![](./media/image126.png)

54. Select **Entity type properties**, review the properties (**TicketID**, **CustomerID**, **Issue**, **TicketStatus**, **CreatedDate**), and select **Create**. When **Entity type updated successfully** appears, select **Cancel**.

![](./media/image127.png)

55. Select **Define entity type key**, select **TicketID**, and select **Save**.

![](./media/image128.png)

**Checkpoint:** The **Explorer** on the configuration canvas lists seven entity types: **Customer**, **Products**, **SalesOrder**, **OrderItem**, **Shipment**, **RefundClaim** and **SupportTicket**, as shown in the table at the start of this task.

### Task 6: Create the relationship types

A **relationship type** connects an origin entity type to a target entity type. In this lab, you link them through properties: the **origin property** is the column on the origin entity that holds the target's key, and the **target property** is the target's key.

| **Relationship** | **Origin entity type** | **Origin property** | **Target entity type** | **Target property** |
|----|----|----|----|----|
| placedBy | SalesOrder | CustomerID | Customer | CustomerID |
| partOf | OrderItem | OrderID | SalesOrder | OrderID |
| forProduct | OrderItem | ProductID | Products | ProductID |
| tracks | Shipment | OrderID | SalesOrder | OrderID |
| refundFor | RefundClaim | OrderID | SalesOrder | OrderID |
| raisedBy | SupportTicket | CustomerID | Customer | CustomerID |

**Important:** The origin property and the target property must hold the same values (for example, **C001** on both sides). If you choose a column with different values, the relationship is created but finds no matches.

1.  In the **Explorer**, select **SalesOrder**, and then select **Add relationship** from the top ribbon.

![](./media/image129.png)

2.  Enter the following details, and then select **Create**.

| **Relationship type name** | +++placedBy+++ |
|----|----|
| **Origin entity type** | **SalesOrder** |
| **Target entity type** | **Customer** |

![](./media/image130.png)

3.  The relationship appears on the canvas between **SalesOrder** and **Customer**.

![](./media/image131.png)

4.  Select the **placedBy** relationship to open its configuration.

![](./media/image132.png)

5.  Leave **Use mapping table?** set to **Off**. Under the origin entity type **SalesOrder**, in **Property**, select **CustomerID**. Under the target entity type **Customer**, in **Property**, select **CustomerID**. Select **Save**.

![](./media/image133.png)

**Note:** The screenshot shows the target property **customer_id** from an earlier version of the data file. Select **CustomerID**.

6.  When **Successfully updated the relationship type** appears, select **Cancel**.

![](./media/image134.png)

7.  Select **Home** to return to the canvas.

![](./media/image135.png)

8.  In the **Explorer**, select **OrderItem (1)**, and then select **Add relationship**. Enter +++partOf+++ **(2)**, select **OrderItem** as the origin **(3)** and **SalesOrder** as the target **(4)**, and select **Create (5)**.

![](./media/image136.png)

9.  On the canvas, select the **partOf** relationship.

![](./media/image137.png)

10. Leave **Use mapping table?** set to **Off**. Set the origin **Property** to **OrderID** and the target **Property** to **OrderID**, and then select **Save**.

![](./media/image138.png)

11. When **Successfully updated the relationship type** appears, select **Cancel**.

![](./media/image139.png)

12. Select **Home**, and then select **Add relationship**.

![](./media/image140.png)

13. Enter +++forProduct+++, select **OrderItem** as the origin and **Products** as the target, and select **Create**.

![](./media/image141.png)

14. On the canvas, select the **forProduct** relationship.

![](./media/image142.png)

15. Set the origin **Property** to **ProductID (1)** and the target **Property** to **ProductID (2)**. Select **Save (3)**, and then select **Cancel (4)**.

![](./media/image143.png)

16. Select **Home**, select **Add relationship**, enter +++tracks+++, select **Shipment** as the origin and **SalesOrder** as the target, and select **Create**.

![](./media/image144.png)

17. On the canvas, select the **tracks** relationship.

![](./media/image145.png)

18. Set the origin **Property** to **OrderID** and the target **Property** to **OrderID**. Select **Save**, and then select **Cancel**.

![](./media/image146.png)

19. Select **Home**, select **Add relationship**, enter +++refundFor+++, select **RefundClaim** as the origin and **SalesOrder** as the target, and select **Create**.

![](./media/image147.png)

20. On the canvas, select the **refundFor** relationship.

![](./media/image148.png)

21. Set the origin **Property** to **OrderID** and the target **Property** to **OrderID**. Select **Save**, and then select **Cancel**.

![](./media/image149.png)

22. Select **Home**, select **Add relationship**, enter +++raisedBy+++, select **SupportTicket** as the origin and **Customer** as the target, and select **Create**.

![](./media/image150.png)

23. On the canvas, select the **raisedBy** relationship.

![](./media/image151.png)

24. Set the origin **Property** to **CustomerID** and the target **Property** to **CustomerID**. Select **Save**, and then select **Cancel**.

![](./media/image152.png)

25. Select **Home**. Verify that the canvas shows six relationship types connecting the seven entity types.

![](./media/image153.png)

**Tip:** You can also turn **Use mapping table?** to **On** and link the entities through a mapping table: select the table that holds both keys (for example, **orderitems** for *partOf*), and then select the column that matches each entity's key (**OrderItemID** and **OrderID**). This is the method used in the Microsoft Learn tutorial.

26. On the configuration canvas, select an entity type (for example, **SupportTicket**), and then select **View Entity Type details** on the ribbon.

![](./media/image154.png)

27. Verify that the **Entity type key** is set, the **Data source** points to the correct table, and the properties match the table in Task 5. In the **Relationships** pane, select the expand icon to see the entity's relationships.

![](./media/image155.png)

### Task 7: Ask questions with the Ontology agent

1.  On the **Home** tab, select **Ontology agent**.

![](./media/image156.png)

2.  In the **Ontology Agent** pane, enter +++Which table links OrderItem to Products?+++ and select the **Send** icon.

![](./media/image157.png)

3.  Review the answer. The agent identifies **dbo.orderitems** as the linking table and the direct relationship **forProduct**.

![](./media/image158.png)

4.  Enter +++What did John_Doe order, and what is its shipment status?+++ and select **Send**.

![](./media/image159.png)

5.  Review the answer. The agent follows the relationships from **Customer** to **SalesOrder**, **OrderItem** and **Shipment** to return the order, the item and the shipment status.

![](./media/image160.png)

**Note:** The Ontology agent is in preview, and AI-generated answers may be incorrect. Check important answers against the source tables.

## Exercise 3: Build the unified customer resolution agent

In this exercise, you configure the **IQAgent** agent in Microsoft Foundry with instructions, and connect it to Foundry IQ (policy documents), Work IQ (email) and Fabric IQ (the ontology).

### Task 1: Add instructions to the agent

1.  Open the Azure portal at +++https://portal.azure.com/+++ and sign in with your lab credentials if prompted.

2.  Select the **AgenticAI** resource group.

![](./media/image168.png)

3.  Select the **agentic-ai-project-@lab.LabInstance.Id** Foundry project.

![](./media/image169.png)

4.  On the **Overview** pane, click on **Go to Foundry portal**.

![](./media/image170.png)

**Note:** If you are prompted to select a project in the Microsoft Foundry portal, select the project you created earlier.

![](./media/image171.png)

5.  Select **Build**.

![](./media/image172.png)

6.  In the **Agents** section, select the **IQAgent** agent.

![](./media/image173.png)

![](./media/image174.png)

7.  In the **Instructions** section, enter the following text to define the agent's behavior.

```text
You are Contoso's Resolution Agent for customer shipment and delivery issues.

Your job is to:
1. Review customer and internal emails to understand the issue and urgency.
2. Use Fabric IQ to validate customer, order, inventory, shipment, and support facts.
3. Use Foundry IQ to apply Contoso's internal policies, SLA guidance, escalation criteria, and communication standards.
4. Recommend the best next action based on both data and policy.
5. Draft clear, professional customer-facing or internal responses when requested.

Always:
- Validate facts using available business data before making a recommendation.
- Use policy documents when deciding replacement, refund, escalation, or SLA handling.
- Distinguish between confirmed facts, likely causes, and recommended actions.
- If inventory is available and policy supports replacement, prioritize fast resolution for Premium customers.
```

![](./media/image175.png)

8.  Click on **Save**.

![](./media/image176.png)

![](./media/image177.png)

### Task 2: Connect Foundry IQ (policy documents)

1.  In the **Knowledge** section, select **Add**, and then choose **Connect to Foundry IQ**.

![](./media/image178.png)

2.  In the **Connect to Foundry IQ** window, select **Connect to an AI Search resource**.

![](./media/image179.png)

3.  Select **searchleaves@lab.LabInstance.Id (1)** as the **Foundry IQ resource**, make sure **API Key (2)** is selected as the authentication type, and then click on **Connect (3)**.

![](./media/image180.png)

4.  Click on **Create a knowledge base**, keep the default name, select **gpt-5** as the **Chat completions model**, and scroll down.

![](./media/image181.png)

![](./media/image182.png)

5.  Click on **Add Sources** and select **Azure Blob Storage** from the list.

![](./media/image183.png)

![](./media/image184.png)

6.  In the **Choose a knowledge type** window, select the **storage@lab.LabInstance.Id** storage account and the **document** container you created earlier. Select **gpt-5** as the **Chat completions model**, and then click on **Create**.

![](./media/image185.png)

**Note:** If the **gpt-5** model is not available in the **Chat completions model (5)** list, select **gpt-5.2** instead, and then click on **Create (6)**.

7.  Make sure the knowledge source shows the **Active** status (wait about 5 minutes or refresh the page), and then select **Save knowledge base**.

![](./media/image186.png)

**Note:** If the status is not displayed as **Active**, refresh the page once and check the status again.

8.  Select **Use in an agent**, and then choose the **IQAgent** agent to associate the knowledge base with it.

![](./media/image187.png)

![](./media/image188.png)

### Task 3: Connect Work IQ (email)

1.  In the **Tools** section, select **Add**, and then choose **Browse all tools**.

![](./media/image189.png)

2.  On the **Catalog** tab, search for +++Work IQ+++, select **Work IQ Mail**, and then click on **Create**.

![](./media/image190.png)

3.  In the **Connect the Work IQ Mail tool** window, review the default settings and select **Connect**.

![](./media/image191.png)

4.  Verify that **Work IQ Mail** is connected successfully.

![](./media/image192.png)

### Task 4: Connect Fabric IQ (ontology)

1.  In the **Tools** section, select **Add**, and then choose **Browse all tools**.

![](./media/image193.png)

2.  In the **Select a tool** pane, on the **Configured** tab, select **Fabric IQ (OneLake Catalog)**, and then select **Add tool**.

![](./media/image161.png)

3.  In the **OneLake Catalog**, select **NetworkOperationsOntology**, and then select **Add**.

![](./media/image162.png)

**Note:** When you connect a non-Foundry tool, customer data may be sent outside the Azure compliance boundary. Review the notice in the **Select a tool** pane with your administrator.

4.  Verify that **Fabric IQ (NetworkOperationsOntology)** appears under **Tools**, and then select **Save**.

![](./media/image163.png)

5.  Verify that **Fabric IQ** and **Work IQ Mail** are connected successfully.

![](./media/image194.png)

## Exercise 4: Test the customer resolution agent

In this exercise, you send sample customer and internal emails to your mailbox, and then ask the agent to analyze the issue, check the data and policies, and draft a response.

### Task 1: Send the demo emails

1.  Open a new browser tab and navigate to Outlook: +++https://outlook.office.com/+++

2.  Sign in with the following credentials.

| **Username** | **+++@lab.CloudPortalCredential(User1).Username+++** |
|----|----|
| **Password** | **+++@lab.CloudPortalCredential(User1).Password+++** |

3.  In Outlook, select **New mail (1)** to create a new email.

![](./media/image195.png)

4.  In the **To (1)** field, enter +++@lab.CloudPortalCredential(User1).Username+++, enter the subject and body of **Email 1** below, and then click on **Send (4)**.

**Email 1**

| **Subject** | +++Urgent: Missing and Damaged Devices in Order O5001+++ |
|----|----|

```text
Hello Team,

We received our order O5001 for 25 Contoso ProBook 14 laptops today.

However, only 18 units were delivered, and out of those, 4 units appear to be physically damaged on arrival. We are onboarding a new office team this Friday, so this delay is creating a serious operational issue for us.

Please investigate and let us know how soon the missing and damaged units can be resolved.

Regards,
Ritika Sharma
IT Procurement Lead
Apex Legal Solutions
```

![](./media/image196.png)

5.  Repeat step 3 and step 4 to send **Email 2** and **Email 3** to the same address.

**Email 2**

| **Subject** | +++Fwd: Urgent customer issue - Apex Legal / O5001+++ |
|----|----|

```text
Team,

Apex Legal is one of our premium enterprise customers. Please review this immediately.

They are onboarding a new office and cannot afford delays. If replacement inventory is available, we should prioritize expedited fulfillment.

Can someone confirm what happened with this shipment and draft a response for the customer today?

Thanks,
Maya
Account Manager
```

**Email 3**

| **Subject** | +++Shipment exception review for O5001+++ |
|----|----|

```text
Initial shipment scan indicates carton count discrepancy for order O5001.

There may have been a warehouse packing issue involving 7 units not loaded into the outbound pallet. A separate damage note was also recorded during final-mile delivery for 4 units.

Pending final confirmation.
```

6.  Open the **Inbox** and verify that the three emails have been received.

![](./media/image197.png)

### Task 2: Chat with the agent

1.  Return to the Microsoft Foundry portal and open the **IQAgent** playground. In the chat pane, enter the following prompt and send it.

> +++Review the latest Apex Legal email and summarize.+++

![](./media/image198.png)

2.  When prompted, select **Approve** to grant the required permissions.

![](./media/image199.png)

3.  Select **Always approve this tool**.

![](./media/image200.png)

4.  Enter the following prompt and review the response. The agent checks the policy documents to decide whether a replacement applies.

> +++Is this customer eligible for replacement based on our policy?+++

![](./media/image201.png)

5.  Enter the following prompt and review the response.

> +++Should this issue be escalated?+++

![](./media/image202.png)

6.  Enter the following prompt and review the drafted response.

> +++Draft a customer response based on the issue and our communication standards.+++

![](./media/image203.png)

7.  Enter the following prompt to query the ontology through Fabric IQ, and select the **Send** icon.

> +++Who placed order 101, and what did they buy?+++

![](./media/image164.png)

8.  Review the answer. The agent returns the customer and the items, with citations to the ontology.

![](./media/image165.png)

9.  Enter the following prompt and select **Send**.

> +++Order 103's refund is pending because of late delivery. Check its shipment details and tell me what the SOP says to do.+++

![](./media/image166.png)

10. Review how the agent combines the facts from the ontology with the guidance from the knowledge base.

![](./media/image167.png)

**Summary**

In this use case, you built an end-to-end **AI-powered customer resolution agent** by combining data, knowledge and communication tools. You created an Azure AI Search service and a storage account with Contoso's policy documents, built a Fabric lakehouse and an ontology that models customers, products, orders, shipments, refund claims and support tickets, and created a Foundry agent connected to **Work IQ** (email), **Foundry IQ** (policies) and **Fabric IQ** (the ontology). The agent can analyze customer complaints, validate order and shipment details, apply organizational policies, recommend the best course of action and draft professional responses. This shows how organizations can move from reactive support processes to proactive, data-driven decision-making that improves resolution time, accuracy and customer experience.
