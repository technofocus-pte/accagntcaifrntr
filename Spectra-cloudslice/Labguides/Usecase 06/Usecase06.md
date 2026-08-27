<!--
lab:
  title: Use case 6 - Build an intelligent banking assistant with MCP tools and Microsoft Agent Framework
  description: 'By implementing this use case, you will:'
  duration: 10 minutes
  level: 200
  islab: true
-->

# Use case 6 - Build an intelligent banking assistant with MCP tools and Microsoft Agent Framework

## Introduction

In modern banking, customers expect quick, intuitive, and personalized services without navigating complex applications. Traditional banking interfaces often require multiple steps to perform simple tasks like checking balances, viewing transactions, or making payments.

This use case demonstrates how an **AI-powered Banking Assistant Agent** simplifies these interactions through a conversational interface. Users can communicate in natural language, and the system intelligently interprets their requests and routes them to specialized agents.

The solution is built using a **multi-agent architecture**, where each agent handles a specific banking function such as account management, transaction retrieval, and payment processing. An orchestrator coordinates these agents to deliver accurate, real-time responses, creating a seamless and efficient digital banking experience.

### Objectives

By implementing this use case, you will:
- Understand how to design a **multi-agent AI system** for real-world
  applications

- Enable **natural language interaction** for banking operations
- Implement **intelligent request routing** between specialized agents
- Integrate AI agents with **backend banking APIs and services**
- Automate common banking tasks such as:

    - Checking account balances
    - Viewing transaction history
    - Processing payments

- Enhance the system with advanced capabilities like **invoice-based
  payment processing**

- Deliver a **scalable and user-friendly conversational banking
  experience**


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

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image1.png)


1. **Help** tab holds the Support information. The **ID** value here is the **Lab instance ID** which will be used during the lab execution.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image2.png)

    >[!Alert] Make sure you create all your resources under this Resource group.


### Task 1: Register Service provider

1. Open a browser go to +++https://portal.azure.com+++ and sign in with your cloud slice account below.

    Username: +++@lab.CloudPortalCredential(User1).Username+++

    Password: +++@lab.CloudPortalCredential(User1).AccessToken+++

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image3.png)

    ![A login box with a red box and blue box with text AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image4.png)

1. Click on **Subscriptions** tile.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image5.png)

1. Click on the subscription name.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image6.png)

1. Expand Settings from the left navigation menu. Click on **Resource providers**, enter +++Microsoft.CognitiveServices+++ and select it, and then click **Register**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image7.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image8.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image9.png)

1. Repeat the steps in #4 to register the following Resource provider.

    - +++Microsoft.AlertsManagement+++


### Task 2: Retrieve resource group name and location

1. Type in +++Resource group+++ in the search bar and select **Resource groups**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image10.png)

1. Click on your assigned **Resource group**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image11.png)

1. In **Resource group** page, copy **resource group name and location** and paste them in a notepad, then **Save** the notepad to use the information in the upcoming tasks.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image12.png)


### Task 3: Open Github Codespaces environment

1. Open your browser, navigate to the address bar, type or paste the following URL:
  
    +++https://github.com/technofocus-pte/Banking-assistant-Agent+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image13.png)

1. Click on **fork** to fork the repo. Give unique name to the repo and click on **Create repo** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image14.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image15.png)

1. Click on **Code > Codespaces > Codespaces**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image16.png)

1. Wait for the Codespaces environment to setup. It takes few minutes to setup completely

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image17.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image18.png)


### Task 4: Provision Services and deploy application to Azure

1. Run the following command on the Terminal. It generates the code to copy. Copy the code and press Enter.

    +++azd auth login+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image19.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image20.png)

1. Default browser opens to enter the generated code to verify. Enter the code and click **Next**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image21.png)

1. Sign in with your Azure credentials.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image22.png)

    ![A screenshot of a computer error AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image23.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image24.png)

1. To create an environment for Azure resources, run the following Azure Developer CLI command and enter the following names:
  
    +++azd env new+++
  
    environment name: +++bagent@lab.LabInstance.Id+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image25.png)

1. Run below command to provision the services to Azure, build your container.

    +++azd env set AZURE_RESOURCE_GROUP AgenticAI+++
  
    +++azd env set Azure_Location JapanEast+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image26.png)

1. Run azd up - This will provision Azure resources

    +++azd up+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image27.png)

1. Select below values.

    - **Select an Azure Subscription to use**: @lab.CloudSubscription.Name
    - **azureAiServiceLocation**: @lab.CloudResourceGroup(AgenticAI).Location
    - **‘location' infrastructure parameter:** Central US
    - **Pick a resource group to use:** @lab.CloudResourceGroup(AgenticAI).Name
  
    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image28.png)
  
    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image29.png)


1. This deployment will take *7-10 minutes* to provision the resources in your account and set up the solution with sample data.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image30.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image31.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image32.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image33.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image34.png)

1. The service account endpoint has been completed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image35.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image36.png)

1. The service backend has been completed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image37.png)

1. The service payment has been completed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image38.png)

1. The service transaction has been completed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image39.png)

1. The service web has been completed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image40.png)


### Task 5: Verify deployed resources in the Azure portal

1. Select **Resource groups**

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image41.png)

1. Click on your assigned **Resource group**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image42.png)

1. Make sure all the resources got deployed successfully

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image43.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image44.png)

1. Make sure the below resource got deployed successfully

    - Foundry
    - Foundry project
    - Account Container App
    - Backend Container App
    - Payment Container App
    - Transaction Container App
    - Web Container App
    - Document Intelligence
    - Container App Environment
    - Azure Cosmos DB account
    - Search service
    - Azure Storage account

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image45.png)


1. Select **Foundry project**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image46.png)

1. Click **Go to Foundry portal** to verify that the model has been successfully deployed.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image47.png)

1. In Microsoft Foundry, navigate to the **Build** section from the top menu to start creating and managing your AI solutions.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image48.png)


### **Task 6: ** **Test the Application**

1. Click on the generated **service web endpoint URL** to open and access the deployed application in your browser.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image49.png)

1. Click on **Open** button

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image50.png)

1. Click on **Start banking**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image51.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image52.png)

1. On the Banking Assistant home page, select **Transaction Analysis** to view and analyze transaction details.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image53.png)

1. Select **Start Chat** to initiate a conversation with the Banking Assistant.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image54.png)

1. Click **Review Card Spend** to analyze and review card transaction spending details.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image55.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image56.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image57.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image58.png)


### Task 7: Delete the resources

1. From the Azure portal home page, select the assigned Resouce group. Select all the resources under the Resource group and select Delete.

    ![A screenshot of a computer Description automatically generated](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image59.png)

1. Enter +++delete+++ and click on the **Delete** button to confirm deletion. Click on **Delete** in the Delete confirmation dialog box.

    ![A screenshot of a computer Description automatically generated](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image60.png)

1. Confirm the deletion of all the resources with a success message.

    ![A screenshot of a computer screen Description automatically generated](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2006/media/image61.png)


## Summary

This use case showcases how an AI-driven, multi-agent system can modernize traditional banking by transforming it into a **conversational and intelligent service platform**.

By leveraging specialized agents and orchestration, the solution efficiently handles diverse banking tasks while maintaining accuracy and responsiveness. It reduces user effort, improves accessibility, and enables faster interactions compared to traditional systems.

Overall, the Banking Assistant Agent demonstrates the power of **Generative AI and multi-agent collaboration** in building scalable, efficient, and customer-centric financial solutions.
