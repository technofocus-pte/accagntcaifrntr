<!--
lab:
  title: Usecase 03- Create a cross-department intelligent multi-agent
  description: 'The objective of this use case is to demonstrate how a multi-agent AI system can:'
  duration: 10 minutes
  level: 400
  islab: true
-->

# Usecase 03 - Create a cross-department intelligent multi-agent

## Introduction

Contoso, a growing global technology company, hires dozens of employees every month across multiple regions. Their onboarding process involves coordination between HR, IT, Facilities, Security, and Finance. Each department uses different systems, and onboarding tasks are often managed through email threads, spreadsheets, and manual follow-ups. This leads to delays, missed steps, and a poor first-day experience for new hires.

To modernize this process, Contoso adopts a **Multi-Agent AI Automation framework** where specialized AI agents collaborate to orchestrate onboarding tasks end-to-end.

### Solution architecture

![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/a1.png)

### Agentic architecture

![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/a2.png)

### Objective

The objective of this use case is to demonstrate how a **multi-agent AI system** can:
- Automate cross-department onboarding workflows
- Coordinate tasks between HR, IT, Facilities, and Finance systems
- Dynamically generate and execute task plans based on new hire details
- Reduce manual effort, delays, and human error
- Provide real-time visibility into onboarding progress
- Ensure a seamless and consistent first-day experience for employees


### Prerequisites

- **GitHub Account**: You are expected to have your own GitHub login
  credentials. If you do not have an account, please create one by visiting: +++https://github.com/signup?user_email=&source=form-home-signup+++


### Task 0: Understand the VM and the credentials

In this task, we will identify and understand the credentials that we will be using throughout the lab.

1. **Instructions** tab hold the lab guide with the instructions to be followed throughout the lab.

1. **Resources** tab has got the credentials that will be needed for executing the lab.

    - **URL** – URL to the Azure portal
    - **Subscription** – This is the ID of the subscription assigned to
    you

    - **Username** – The user id with which you need to login to the
    Azure services.

    - **Password** – Password to the Azure login. Let us call this
    Username and password as Azure login credentials. We will use these creds wherever we mention Azure login credentials.

    - **Resource Group** – The **Resource group** assigned to you.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image3.png)


1. **Help** tab holds the Support information. The **ID** value here is the **Lab instance ID** which will be used during the lab execution.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image4.png)

    >[!Alert] Make sure you create all your resources under this Resource group


### Task 1: Register Service provider

1. Open a browser go to +++https://portal.azure.com+++ and sign in with your cloud slice account below.

    Username: +++@lab.CloudPortalCredential(User1).Username+++

    Password: +++@lab.CloudPortalCredential(User1).AccessToken+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image5.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image6.png)

1. Click on **Subscriptions** tile.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image7.png)

1. Click on the subscription name.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image8.png)

1. Expand Settings from the left navigation menu. Click on **Resource providers**, enter +++Microsoft.CognitiveServices+++ and select it, and then click **Register**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image9.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image10.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image11.png)


### Task 2: Open Github Codespaces environment

1. Open your browser, navigate to the address bar, type or paste the following URL: +++https://github.com/technofocus-pte/MultiAgent-CustomAutomatiSolution-Acceleratoron-Engine+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image12.png)

1. Click on **fork** to fork the repo. Give unique name to the repo and click on **Create repo** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image13.png)

1. Click on **Code > Codespaces > Codespaces+**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image14.png)

1. Wait for the Codespaces environment to setup .It takes few minutes to setup completely

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image15.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image16.png)


### Task 3: Provision Services and deploy application to Azure

1. Run the following command on the Terminal. It generates the code to copy. Copy the code and press Enter.

    +++azd auth login+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image17.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image18.png)

1. Default browser opens to enter the generated code to verify. Enter the code and click **Next**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image19.png)

1. Sign in with your Azure credentials.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image20.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image21.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image22.png)

1. Run azd up - This will provision Azure resources

    +++azd up+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image23.png)

1. To create an environment for Azure resources, enter: +++macaedev@lab.LabInstance.Id+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image24.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image25.png)

1. Select below values.

    - **Select an Azure Subscription to use** : Select your subscription
    - **azureAiServiceLocation**: Sweden Central
    - **‘location' infrastructure parameter:** Central US
    - **Pick a resource group to use:** AgenticAI

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image26.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image27.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image28.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image29.png)


1. This deployment will take *7-10 minutes* to provision the resources in your account and set up the solution with sample data.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image30.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image31.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image32.png)

1. Now the deployment is complete

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image33.png)

1. After the application has been successfully deployed, you see a URL displayed in the terminal. Copy the **Frontend application URL**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image34.png)


### Task 4: Post-Deployment Configuration

1. Run the sample data processing script by executing **bash infra/scripts/selecting_team_config_and_data.sh** from the project root to prepare and upload the required data.

    +++bash infra/scripts/selecting_team_config_and_data.sh+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image35.png)

1. After running the command **bash infra/scripts/selecting_team_config_and_data.sh**, authenticate in the browser by opening +++https://microsoft.com/devicelogin+++ and entering the **displayed code** to continue the script execution.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image36.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image37.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image38.png)

1. Select your subscription

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image39.png)

1. After running the script, a list of available use case scenarios will appear for selection. You can choose specific scenarios or deploy all use cases at once. Based on your selection, the required datasets and configuration files for those use case(s) will be uploaded to your Azure environment. For this lab, select **6**.
  
    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image40.png)  

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image41.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image42.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image43.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image44.png)


### Task 5: Verify deployed resources in the Azure portal

1. Open a browser go to +++https://portal.azure.com+++ and sign in with your cloud slice account.

1. Select **Resource groups**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image45.png)

1. Click on your assigned **Resource group**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image46.png)

1. Make sure the below resource got deployed successfully

    - Foundry
    - Foundry project
    - App Service
    - Container registry
    - Azure Cosmos DB account
    - Container App
    - SQL Database
    - Search service
    - Azure Storage account

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image47.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image48.png)


1. On the resource group and click on **Azure Storage account.**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image49.png)

1. From the left navigation menu, click on **Containers** , Make sure data should be deployed successfully

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image50.png)

1. Go back to resorcegroup and click on **Foundry Project.**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image51.png)

1. Click **Go to Foundry portal** to verify that the model has been successfully deployed.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image52.png)  

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image53.png)


### Task 6: Add Authentication in Azure App Service configuration

1. Go back to resourcegroup and click on **App Service(+++app-macaedev@lab.LabInstance.Id+++).**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image54.png)

1. On the web app home page, go to **Settings** and click **Authentication** from the left menu

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image55.png)

1. Click on **Add identity provider** to see a list of identity providers.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image56.png)

1. Click on Identity Provider dropdown to see a list of identity providers and select the first option **Microsoft** from the drop-down list

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image57.png)

1. Select **client secret expiration** under App registration and click on **Add** button

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image58.png)

1. You have successfully added app authentication, and now required to log in to access the application.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image59.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image60.png)

1. On the web app home page, go to **Overview** and click **Browse**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image61.png)

1. Wait for the web application deployment to complete.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image62.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image63.png)


### Task 7: Review and Explore the Sample Questions for Your Copilot Application

1. Select the Team option from the top-left section, then click Continue after choosing the desired team.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image64.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image65.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image66.png)


### Task 8: Retail Scenario

In this Retail scenario, Contoso’s Retail Support Team uses a multi-agent AI system to improve customer satisfaction. When a customer shows signs of dissatisfaction — such as poor feedback, repeated complaints, or low engagement — the system analyzes the situation and automatically proposes a recovery plan.

This process is powered by multiple AI agents working together to understand customer history, analyze sentiment, and recommend corrective actions.

1. Select the Retail team, follow the prompts below.

    **Agents Used:** Customer, Order, Analysis Recommendation

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image67.png)

1. In the **Multi-Agent Planner**, under *Quick tasks*, select ***Satisfaction Plan* to generate an analysis of Emily Thompson’s satisfaction with Contoso along with recommended actions to improve it**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image68.png)

1. Click the **Submit** icon as shown in the image.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image69.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image70.png)

1. Task: Click **"Approve Task Plan"** Button

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image71.png)

    **Observe**: *It goes into "Thinking Process", "Processing your plan" and "coordinating with AI Agents".* *Review the output.*

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image72.png)


### Task 9: Product Marketing Scenario

In this scenario, Contoso’s Product Marketing Team uses a multi-agent AI system to quickly generate a professional press release for a product announcement. Instead of manually coordinating between product managers and marketing writers, AI agents collaborate to gather product information, shape the messaging, and produce a structured communication plan.

This scenario demonstrates how AI agents streamline marketing content creation while ensuring alignment with product details and brand voice.

1. Select the Marketing team, follow the prompts below.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image73.png)

    **Agents Used:** Product, Marketing , Proxy

1. Switch to **"Product Marketing Team"** from the top left section and click **"Continue"** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image74.png)

    - Task: From the Quick Tasks, select **"Draft a press release"** and
    submit it.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image75.png)


1. Click the **Submit** icon as shown in the image.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image76.png)

    >[!Note] Average response time is 15–20 seconds.* *Observe: It will trigger the "Generating Plan Action" and give the Proposed Plan with 4 or more Steps*

    - Task: Click on **"Approve Task Plan"** Button

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image77.png)

    >[!Note] Average response time is around 01 minute.* **Observe***:* It goes into "Thinking Process" and observe a spinner "Processing your plan and coordinating with AI Agents". Review the output.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image78.png)


### Task 10: HR Onboarding Scenario

In this scenario, Contoso’s Human Resources Team uses a multi-agent AI system to streamline the onboarding of a new employee. Instead of manually coordinating with IT, facilities, and payroll teams, AI agents collaborate to collect required details, plan onboarding tasks, and prepare everything needed for the employee’s first day.

This demonstrates how AI agents can orchestrate cross-functional onboarding activities efficiently and accurately

1. Select the HR team, follow the prompts below.

    **Agents Used:** HR Helper, Technical support , Proxy

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image79.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image80.png)

1. The HR Onboarding Scenario allows users to explore and retrieve information related to OnBoarding the Employee. Key tasks include:

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image81.png)

    Sample operation:
  
    1. Task: Switch to the **"Human Resources Team"** from the top left section and click **"Continue"**
  
    1. Task: From the Quick Tasks, select **"Onboard New Employee"** and submit it.
  
    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image81.png)
  
    1. Click the **Submit** icon as shown in the image.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image82.png)

    >[!Note] Average response time is 15–20 seconds.
  
    **Observe:** If it asks for additional clarification (Human in the loop) Please provide this information irrespective of what specific information is asked. This will prevent agent for asking for multiple clarifications

    ```
    **department**: hr, role: manager, start date: 11/23/2025, orientation
    date: 11/25/2025, location: onsite, email: js@contoso.com, mentor: Jim
    Shorts, benefits package: standard, ID Card: yes, salary: 70000, Laptop
    : Dell 14 Plus
    ```
  
    *Observe: It will trigger "Generating Plan Action" and "Proposed Plan" with 4 or more Steps*
  
    **Task**: Click on **"Approve Task Plan"** Button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image83.png)

    >[!Note] Average response time is around 01 minute 15 seconds. Observe: It goes into "Thinking Process", "Processing your plan" and "coordinating with AI Agents" Review the output.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image84.png)


### Task 11: RFP Analysis Scenario

In this scenario, Contoso’s RFP Team uses a multi-agent AI system to analyze Request for Proposal (RFP) and contract documents. Reviewing RFPs manually can take days and involves multiple stakeholders such as legal, compliance, and business teams. With AI agents working together, the system summarizes the document, identifies risks, and checks compliance requirements — helping teams respond faster and more accurately

1. Select the RFP team, follow the prompts below.

    **Agents Used:** RFP Summary, RFP Risk, RFP Compliance

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image85.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image86.png)

    The RFP Analysis Scenario allows users to explore and analyze Request for Proposal (RFP) and contract documents. Key tasks include:
  
    *Sample operation:*

    - **Task**: Switch to the **"RFP Team"** from the top left section and
    click **"Continue"** button.
  
    - **Task**: From the Quick Tasks, select **"RFP Document Summary"** and
    submit it.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image87.png)


1. Click the **Submit** icon as shown in the image.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image88.png)

    >[!Note] Average response time is 10–15 minutes.
  
    **Observe**: It will trigger the "Generating Plan Action" and give the Proposed Plan with 5 or more Steps

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image89.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image90.png)


### Task 12: Contract Compliance Review Scenario

In this scenario, Contoso’s Contract Compliance Review Team uses a multi-agent AI system to analyze Non-Disclosure Agreements (NDAs) and other contract documents. Legal and compliance teams often spend significant time reviewing contracts for risks, missing clauses, and policy alignment. With AI agents collaborating, the system can quickly summarize contracts, identify risks, and verify compliance with internal standards.

This scenario highlights how AI supports faster, more consistent contract reviews while keeping humans in control of final decisions.

1. Select the Contract Compliance team, follow the prompts below.

    **Agents Used:** Contract Summary, Contract Risk, Contract Compliance

    The Contract Compliance Review Scenario allows users to explore and analyze NDA and contract documents for compliance and risk assessment. Key tasks include:

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image91.png)

    Sample operation:
    - **Task**: Switch to the **"Contract Compliance Review Team"** from the
    top left section and click **"Continue"** button.
  
    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image92.png)
  
    - **Task**: From the Quick Tasks, select **"NDA Contract Review"** and
    submit it.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image93.png)


1. Click the **Submit** icon as shown in the image.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image94.png)

    >[!Note] Average response time is 10–15 minutes.* **Observe***:* It will trigger the "Generating Plan Action" and give the Proposed Plan with 4 or more Steps

    - Task: Click on **"Approve Task Plan"** Button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image95.png)

    >[!Note] Average response time is around 01 minute. **Observe**: It goes into "Thinking Process", "Processing your plan" and "coordinating with AI Agents". **Review the output.**
  
    This structured approach ensures that users receive automated, AI-coordinated task execution and intelligent responses from specialized agents.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image96.png)


### Task 12: Delete the Resources

1. To delete Resource group , type **Resource groups** in the Azure portal search bar, navigate and click on **Resource groups** under **Services**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image97.png)

1. In the Resource groups page, select your resource group.

1. In the **Resource group** home page, select all resources and click on **delete**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image98.png)

1. In the **Delete Resources** pane that appears on the right side, navigate to **Enter “delete” to confirm deletion** field, then click on the **Delete** button

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image99.png)

1. On **Delete confirmation** dialog box, click on **Delete** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2003/media/image100.png)


### Summary

In this use case, Contoso leverages a Multi-Agent Accelerator solution deployed on Azure to orchestrate employee onboarding. When HR initiates a new hire request, AI agents collaborate to analyze requirements, create a task plan, and coordinate actions across enterprise systems.

Specialized agents handle responsibilities such as account provisioning, hardware allocation, access control, payroll setup, and compliance verification. A planner agent breaks the goal into structured steps, executor agents perform actions, and validation agents ensure completeness and policy alignment — all while keeping humans in the loop for approvals.

This implementation highlights how multi-agent AI orchestration transforms a traditionally manual, error-prone HR process into an intelligent, automated, and scalable workflow. The result is faster onboarding, improved operational efficiency, and a better experience for both employees and internal teams.
