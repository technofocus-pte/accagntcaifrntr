## Usecase 2- Building multi agent AI solution for streamlining Healthcare prior authorization workflows 

**Introduction**

In today’s rapidly evolving digital landscape, enterprises like
**Contoso Ltd.** face increasing pressure to streamline operations,
improve decision-making, and scale intelligent automation across
departments. Traditional automation approaches often fall short when
dealing with **complex, cross-functional workflows**, where multiple
systems, teams, and data sources must be coordinated efficiently.

To address these challenges, Contoso adopts the **Multi-Agent Solution
Accelerator**, an advanced AI-driven framework that leverages multiple
specialized agents working collaboratively to execute business
processes.

This accelerator enables organizations to design **intelligent,
agent-based workflows**, where each AI agent is responsible for a
specific function—such as data retrieval, reasoning, validation, and
execution. These agents operate in a coordinated manner, orchestrated
through a central system that interprets user requests and dynamically
assigns tasks.

Built on modern cloud technologies like **Azure OpenAI Service**,
**Azure Cosmos DB**, and containerized microservices, the solution
provides a scalable and extensible foundation for enterprise AI
applications.

**Business Scenario**

Contoso operates across multiple business units including **supply
chain, finance, customer service, and compliance**. Each department
relies on different systems and processes, resulting in:

- Fragmented workflows across departments

- Manual coordination causing delays and inefficiencies

- High risk of human errors in decision-making

- Limited scalability of automation initiatives

To overcome these challenges, Contoso implements a **multi-agent AI
system** where:

Multi-Agent Workflow

1.  **User Request Intake Agent**  
    Captures business queries (e.g., “Approve supplier contract” or
    “Analyze sales performance”).

2.  **Planning Agent**  
    Breaks down the request into smaller executable tasks.

3.  **Data Retrieval Agent**  
    Fetches relevant data from enterprise systems (ERP, CRM, data
    warehouses).

4.  **Reasoning Agent**  
    Applies AI models to analyze data and generate insights.

5.  **Validation Agent**  
    Ensures accuracy, compliance, and business rule alignment.

6.  **Execution Agent**  
    Triggers actions such as approvals, notifications, or report
    generation.

**Prerequisites**

- **GitHub Account**: You are expected to have your own GitHub login
  credentials.  
  If you do not have an account, please create one by visiting:  
  <https://github.com/signup>

## Task 1: Register Service provider

1.  Open a browser go to +++https://portal.azure.com+++ and sign in with
    your cloud slice account below.

> Username: <+++@lab.CloudPortalCredential>(User1).Username+++
>
> Password: <+++@lab.CloudPortalCredential>(User1). *TAP*+++
>
> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image1.png)
>
> ![A login box with a red box and blue box with text AI-generated
> content may be incorrect.](./media/image2.png)

2.  Click on **Subscriptions** tile.

> ![A screenshot of a computer AI-generated content may be
> incorrect.](./media/image3.png)

3.  Click on the subscription name.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image4.png)

4.  Expand Settings from the left navigation menu. Click on **Resource
    providers**, enter **+++** **Microsoft.CognitiveServices+++** and
    select it, and then click **Register**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image5.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image6.png)

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image7.png)

5.  Repeat the steps \#4 to register the following Resource provider.

- +++**Microsoft.AlertsManagement**+++

- +++Microsoft.App+++

- +++Microsoft.ContainerRegistry+++

- +++Microsoft.OperationalInsights+++

- +++Microsoft.Insights+++

![](./media/image8.png)

## Task 2: Assign Contributor Role

1.  Select **Subscriptions**.

![](./media/image9.png)

2.  From the left menu, click on the **Access control(IAM).**

3.  On the Access control(IAM) page, Click +**Add** and select **Add
    role assignments.**

![](./media/image10.png)

4.  In the Azure “Add role assignment” page, the **Contributor** role is
    selected under **Privileged administrator roles**, and the user
    proceeds by clicking **Next** to continue the assignment
    process.![](./media/image11.png)

5.  In the **Add role assignment** tab, select Assign access to User
    group or service principal. Under Members, click **+Select members**

> ![](./media/image12.png)

6.  On the Select members tab , search your subscription and
    click **Select.**

> ![](./media/image13.png)

7.  In the **Add role assignment** page, Click **Review + Assign**, you
    will get a notification once the role assignment is complete.

> ![](./media/image14.png)
>
> ![](./media/image15.png)

8.  You will see a notification

![](./media/image16.png)

## Task 3: Retrieve resource group name and location

1.  Type in +++**Resource group+++** in the search bar and
    select **Resource groups**.

![A screenshot of a computer AI-generated content may be
incorrect.](./media/image17.png)

2.  Click on your assigned **Resource group**.

![](./media/image18.png)

3.  In **Resource group** page, copy **resource group name and
    location** and paste them in a notepad, then **Save** the notepad to
    use the information in the upcoming tasks.

![](./media/image19.png)

## Task 4: Open Github Codespaces environment

1.  Open your browser, navigate to the address bar, type or paste the
    following URL: 

+++https://github.com/technofocus-pte/MultiAIAgentAccelerator+++

![](./media/image20.png)

2.  Click on **fork** to fork the repo. Give unique name to the repo and
    click on **Create repo** button.

> ![](./media/image21.png)

![](./media/image22.png)

3.  Click on **Code -\> Codespaces -\> Codespaces+**

![](./media/image23.png)

4.  Wait for the Codespaces environment to setup. It takes few minutes
    to setup completely

![](./media/image24.png)

![](./media/image25.png)

5.  The environment is now ready for resource deployment.

> ![](./media/image26.png)

## Task 5: Provision Services and deploy application to Azure

1.  Run the following command on the Terminal. It generates the code to
    copy. Copy the code and press Enter.

> +++azd auth login+++
>
> ![](./media/image27.png)

2.  Run the azd auth login command, copy the displayed authentication
    code, and complete the sign-in process in your browser to
    authenticate your environment.

> ![](./media/image28.png)

3.  Default browser opens to enter the generated code to verify. Enter
    the code and click **Next**.

> ![](./media/image29.png)

4.  Sign in with your Azure credentials.

> ![](./media/image30.png)
>
> ![](./media/image31.png)
>
> ![](./media/image32.png)

9.  Run the az login command, copy the displayed authentication code,
    and complete the sign-in process in your browser to authenticate
    your environment.

> ![](./media/image33.png)

![](./media/image34.png)

![](./media/image30.png)

![](./media/image35.png)

10. Run azd up - This will provision Azure resources

![](./media/image36.png)

11. Enter any name of your choice and press enter (eg
    :+++prior-auth-devXXXX+++)

![](./media/image37.png)

![](./media/image38.png)

12. Select below values.

- **Select an Azure Subscription to use** : Select your subscription

- **Enter a value for existingResourceGroup Name:** existing resource
  group

- **Enter location**: Sweden Central

![](./media/image39.png)

![](./media/image40.png)

![](./media/image41.png)

13. Enter **Y** to proceed with the deployment.

![](./media/image42.png)

![](./media/image43.png)

![](./media/image44.png)

![](./media/image45.png)

14. The deployment process is currently building container images using
    a remote Azure Container Registry (ACR) build.

![](./media/image46.png)

![](./media/image47.png)

15. The frontend container image has been built successfully, and the
    agent-clinical image build process has started in Azure Container
    Registry (ACR).

![](./media/image48.png)

16. Agent-clinical image build process completed and building
    agent-coverage build process has started in Azure Container Registry
    (ACR).

![](./media/image49.png)

17. Agent-coverage image build process completed and building
    agent-compliance build process has started in Azure Container
    Registry (ACR).

> ![](./media/image50.png)

18. Agent-compliance image build process completed and building
    agent-synthesis build process has started in Azure Container
    Registry (ACR).

![](./media/image51.png)

19. Agent-synthesis image build process completed

![](./media/image52.png)

20. Backend and frontend container app updated sucessfully

> ![](./media/image53.png)

21. The agent-synthesis image has been built successfully, container
    apps have been updated, required roles have been ensured, and
    Foundry MCP tool connections have been created successfully.

> ![](./media/image54.png)

22. The deployment has completed successfully, and the frontend and
    backend application URLs, along with the backend health check
    endpoint, are now available for access.

> ![](./media/image55.png)

## Task 6: Verify deployed resources in the Azure portal

1.  Select **Resource groups**

> ![](./media/image56.png)

2.  Click on your assigned **Resource group**.

![](./media/image57.png)

3.  Make sure the below resource got deployed successfully

- Foundry

- Foundry project

- Container App

- Container registry

- Container App Environment

![](./media/image58.png)

4.  Click on **Foundry Project.**

![](./media/image58.png)

5.  Click **Go to Foundry portal** to verify that the agents has been
    successfully deployed.

![](./media/image59.png)

6.  In Microsoft Foundry, navigate to the **Build** section from the top
    menu to start creating and managing your AI solutions.

![](./media/image60.png)

7.  Agents has been successfully deployed

![](./media/image61.png)

8.  Select the **synthesis-agent**.

![](./media/image61.png)

9.  Click on **Start agent deployment** to deploy the synthesis-agent.

![](./media/image62.png)

![](./media/image63.png)

10. Select the **compliance-agent**.

![](./media/image64.png)

11. Click on **Start agent deployment** to deploy the
    **compliance-agent**.

![](./media/image65.png)

![](./media/image66.png)

12. Repeat steps 10 and 11 to run the **coverage-assessment-agent** and
    **clinical-reviewer-agent**.

![](./media/image67.png)

![](./media/image68.png)

![](./media/image69.png)

## **Task 7: Test the Application**

1.  Go back to the codespace and copy the **Frontend URL**; it will be
    used later to launch the application.

![](./media/image70.png)

2.  Run the command +++python scripts/check_agents.py+++ to verify agent
    connections and application health status.

![](./media/image71.png)

![](./media/image72.png)

3.  Run the check_agents.py script to verify agent registration, backend
    health, frontend availability, and tool connections, ensuring all
    checks pass successfully before proceeding with PA request
    submission.

+++python scripts/check_agents.py --version 1+++

![](./media/image73.png)

13. Run the check_agents.py --poll command to continuously monitor agent
    status, ensuring all components like registration, tool connections,
    backend health, and frontend availability remain healthy before
    submitting PA requests.

+++python scripts/check_agents.py –poll+++

![](./media/image74.png)

14. Click on **Frontend**

![](./media/image74.png)

4.  Click on **Open** button

![](./media/image75.png)

![](./media/image76.png)

5.  Click **"Load Sample Case"** to populate the form with demo data

![](./media/image77.png)

6.  Click **"Submit for Review"**

![](./media/image78.png)

7.  Monitor the progress tracker — you should see all 5 phases complete

![](./media/image79.png)

![](./media/image80.png)

8.  Review the agent results in the dashboard tabs (Compliance,
    Clinical, Coverage)

![](./media/image81.png)

15. Click **Accept Recommendation**

![](./media/image82.png)

![](./media/image83.png)

![](./media/image84.png)

![](./media/image85.png)

**Summary**

In this usecase, you successfully built and deployed a **multi-agent
AI-powered healthcare solution** that automates prior authorization
workflows. By integrating multiple intelligent agents, the system
reduces manual intervention, improves operational efficiency, and
ensures accurate, compliant decision-making.

The hands-on experience covered:

- Setting up Azure resources and permissions

- Deploying containerized AI agents

- Orchestrating agent collaboration

- Testing the application with real scenarios

Overall, this use case demonstrates how **multi-agent AI systems can
transform complex healthcare processes** into efficient, scalable, and
intelligent workflows, providing a strong foundation for enterprise AI
adoption.
