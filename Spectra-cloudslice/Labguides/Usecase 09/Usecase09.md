<!--
lab:
  title: Usecase 9 - Implement end to end agent operations for Zava’s shopping assistant in Microsoft Foundry
  description: In this lab, you implemented a complete end-to-end AI solution for a retail assistant using Azure AI Foundry. Starting from environment setup and deployment, you built Cora, enhanced it with search capabilities, and evolved it into a multi-agent system.
  duration: 15 minutes
  level: 400
  islab: true
  primarytopics:
    - Azure
    - Microsoft Foundry
-->

# Usecase 9 - Implement end to end agent operations for Zava’s shopping assistant in Microsoft Foundry

## Introduction

This lab demonstrates how to implement **end-to-end agent operations** using Azure AI Foundry by building an intelligent retail assistant named **Cora** for Zava, a home improvement retailer. It walks through the complete lifecycle of an AI solution—from provisioning Azure resources and deploying applications to building, orchestrating, and evaluating AI agents.

You will gain hands-on experience with Azure services such as **Azure AI Search, Azure AI Agent Service, and model evaluation tools**, enabling you to design scalable, intelligent, and production-ready AI applications.

## Scenario

Zava is a fictional retail company that sells home improvement products such as paints, tools, and hardware. To enhance customer experience, Zava introduces **Cora**, an AI-powered shopping assistant.

Cora helps customers:
- Discover suitable products for their needs
- Compare prices and availability
- Get personalized recommendations (e.g., eco-friendly options)
- Answer product-related queries


As Zava grows, Cora evolves from a **single-agent system** into a **multi-agent architecture**, incorporating specialized agents like:
- Product Inventory Agent
- Customer Service Agent


Additionally, the solution includes **evaluation pipelines** to ensure accuracy, quality, and safety before deployment.

### Objectives

By completing this lab, you will be able to:
- Register required Azure resource providers and set up the environment
- Deploy an AI-powered application using Azure and GitHub Codespaces
- Configure Azure AI Search and create a product index
- Build and interact with a retail AI agent (Cora)
- Implement vector search for product retrieval
- Develop a **multi-agent system** for advanced use cases
- Generate synthetic datasets for testing and evaluation
- Evaluate AI models for performance, quality, and safety
- Apply **GenAIOps practices** for reliable and secure AI deployment


### Task 1: Register Service provider

1. Open a browser go to +++https://portal.azure.com+++ and sign in with your cloud slice account below.

    Username: +++@lab.CloudPortalCredential(User1).Username+++

    Password: +++@lab.CloudPortalCredential(User1).AccessToken+++

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image1.png)

    ![A login box with a red box and blue box with text AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image2.png)

1. Click on **Subscriptions** tile.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image3.png)

1. Click on the subscription name.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image4.png)

1. Expand Settings from the left navigation menu. Click on **Resource providers**, enter +++Microsoft.CognitiveServices+++ and select it, and then click **Register**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image5.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image6.png)

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image7.png)

1. Repeat the steps #4 to register the following Resource provider.

    - +++Microsoft.AlertsManagement+++


### Task 2: Retrieve resource group name and location

1. Type in +++Resource group+++ in the search bar and select **Resource groups**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image8.png)

1. Click on your assigned **Resource group**.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image9.png)

1. In **Resource group** page, copy **resource group name and location** and paste them in a notepad, then **Save** the notepad to use the information in the upcoming tasks.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image10.png)


### Task 3: Open Github Codespaces environment

1. Open your browser, navigate to the address bar, type or paste the following URL: +++https://github.com/technofocus-pte/observeManageScale-agentic-ai-appsFoundry/tree/feb-2026-refresh+++

1. Click on **fork** to fork the repo. Give unique name to the repo and click on **Create repo** button.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image11.png)

1. Click on **Create fork**

1. Click on **Code > Codespaces > Codespaces**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image12.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image13.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image14.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image15.png)


### Task 4: Provision Services and deploy application to Azure

1. Run the following command on the Terminal. It generates the code to copy. Copy the code and press Enter.

    `az login`

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image16.png)

1. Default browser opens to enter the generated code to verify. Enter the code and click **Next**.

    ![A screenshot of a computer error AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image17.png)

1. Sign in with your Azure credentials.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image18.png)

    ![A screenshot of a computer error AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image19.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image20.png)

1. Open a new VS Code Terminal. Complete these steps:

    `cd scripts`

    `./1-setup.sh`

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image21.png)

1. Then complete the interactive steps providing responses like this:

    1. Enter branch name: +++for-release-1.0.4+++

    1. Enter environment name: +++Ignite-PREL13+++

    1. Enter Azure region: +++@lab.CloudResourceGroup(AgenticAI).Location+++

    1. Enter Subscription ID: +++@lab.CloudSubscription.Id+++

    1. Do you want to activate Azure AI Search? (yes/no): yes
  
    1. Enter existing Resource Group Name: +++@lab.CloudResourceGroup(AgenticAI).Name+++
  
    1. Azure OpenAI Service Name: +++aoai@lab.LabInstance.Id+++
  
    1. Storage Account Name: +++st@lab.LabInstance.Id+++
  
    1. Azure AI Search Service Name: +++aisearch@lab.LabInstance.Id+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image22.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image23.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image24.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image25.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image26.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image27.png)

1. In Visual Studio Code, navigate to the scripts > ForBeginners > azd-setup > infra folder, and then open the main.bicep file.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/imga1.png)

1. Replace the existing main.bicep file with the main.bicep file located in C:\Lab Files\Usecase 9

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/imga4.png)

1. Repeat the same process to replace the main.json and main.parameters.json files with the updated versions from C:\Lab Files\Usecase 9.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/imga2.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/imga3.png)

1. Run this script from root of repo - it will create .env with values extracted by Azure CLI. By default it looks for an  resource group but you can override it.

    `cd ForBeginners/.azd-setup`

    `rm -f .env.lock`

    `azd up`

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image28.png)

1. When prompted, type +++y+++ and press Enter to log in to Azure before continuing with the deployment.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image29.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image30.png)

1. Default browser opens to enter the generated code to verify. Enter the code and click **Next**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image31.png)

1. Sign in with your Azure credentials.

    ![A screenshot of a computer AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image18.png)

    ![A screenshot of a computer error AI-generated content may be incorrect.](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image19.png)

1. This deployment will take *12-15minutes* to provision the resources in your account and set up the solution with sample data.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image32.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image33.png)

    >[!Note] Check the deployment status in your resource group to ensure all resources are provisioned successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image34.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image35.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image36.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image37.png)

1. Now the deployment is complete


### Task 5: Interact with Your AI Agent Using Predefined Questions

1. After the application has been successfully deployed, you see a URL displayed in the terminal. Copy the **URL**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image38.png)

1. Click on **Open** button

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image39.png)

1. Wait for the web application deployment to complete.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image40.png)

1. In the **agent-template-assistant** web app page, enter the following text and click on the **Submit icon** as shown in the below image.

    +++Can you help me choose the best tools for painting my house?+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image41.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image42.png)

1. In the **agent-template-assistant** web app page, enter the following text and click on the **Submit icon** as shown in the below image.

    +++What are the cheapest products available?+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image43.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image44.png)

1. In the **agent-template-assistant** web app page, enter the following text and click on the **Submit icon** as shown in the below image.

    +++Suggest eco-friendly paint options?+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image45.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image46.png)

1. In the **agent-template-assistant** web app page, enter the following text and click on the **Submit icon** as shown in the below image.

    +++How much does the Synthetic Brush set cost and do you have it in stock?+++

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image47.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image48.png)


### Task 6: Set up .env variables.

1. Make sure you are authenticated with Azure CLI. We will use this to retrieve and create a .env file based on the scripts/.env.sample format

    `az login`

1. Run this script from root of repo - it will create .env with values extracted by Azure CLI. By default it looks for an +++rg-Ignite-@lab.LabInstance.Id+++ resource group but you can override it.

    >[!Note] Right click on the *1-update-env-selfguided.sh* and select **open in integrated terminal**.

    +++./1-update-env-selfguided.sh+++

1. Enter the resourcegroup @lab.CloudResourceGroup(AgenticAI).Name and select **Enter** to use the default **Agent Name**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image49.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image50.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image51.png)

1. We have Zava data in scripts/customization. Let's create a product index in Azure AI Search. Switch to the scripts/ folder and run the command:

    `python 2-add-product-index.py`

    >[!Alert] You may need to fill out **env variables** in the created new **.env file**.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image52.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image53.png)

1. This will first run an RBAC update script to give this user the right roles and access to make updates.

1. Then it should upload 49 products to a zava-products index with semantic search, in Azure AI Search.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image54.png)


### Task 7: Environment Setup & Validation

In this task, you will configure and validate your development environment. This includes selecting the appropriate Python environment, installing dependencies, and verifying connectivity to Azure services and the Foundry project.

1. Navigate to the **labs/setup/** folder and open the **00-validate-setup.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image55.png)

1. Click **Select Kernel** in the top-right corner of the notebook and choose the appropriate Python environment to run the lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image56.png)

1. If prompted to select the path, then select the **Python** version i.e **3.12.11**

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image57.png)

1. To import required libraries, run the first cell in the notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image58.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image59.png)

1. Click the **Run (▶)** button to execute the cell and verify that all required Azure AI Foundry environment variables are properly set.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image60.png)

1. Click the **Run (▶)** button to execute the cell and validate that all required Azure AI Search configuration variables are correctly set.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image61.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image62.png)

1. Click the **Run (▶)** button to execute the cell and confirm that all embedding model configuration variables are properly set.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image63.png)


### Task 8: Build “Cora for Zava” – An AI-Powered Retail Shopping Assistant Using Azure AI Agent Service

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. Zava offers a wide range of products including paint, power tools, hand tools, hardware, electrical supplies, and plumbing materials. Cora helps customers find products, check inventory, and provides personalized assistance for home improvement projects.

1. Navigate to the **labs/setup/1-agents** folder and open the **11-build-cora-retail-agent.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image64.png)

1. Click the **Run (▶)** button to execute the cell and verify that all required Python packages are installed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image65.png)

1. Click the **Run (▶)** button to execute the cell and load environment variables from the .env file into your notebook.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image66.png)

1. Click the **Run (▶)** button to execute the cell and confirm that all required environment variables are loaded and ready.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image67.png)

1. Click the **Run (▶)** button to execute the cell and establish a connection to Azure AI Foundry using the configured credentials.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image68.png)

1. Click the **Run (▶)** button to execute the cell to create Cora agent
  
    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image69.png)  

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image70.png)

1. The notebook cell successfully uploads paint product files from the specified folder, showing a confirmation message that 10 files were uploaded after execution.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image71.png)

1. The notebook cell reads and displays the uploaded paint product files, listing each file name along with its product title and price extracted from the file content.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image72.png)

1. The cell executes successfully, creating a vector store named +++"Zava-Paint-Products"+++ using the uploaded files, and confirms that the vector store was created with 10 files.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image73.png)

1. Run the cell to update the agent by attaching the file search tool, enabling it to query and retrieve information from the created vector store of uploaded product files.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image74.png)

1. Run the cell to create a new conversation thread and display a confirmation message indicating that the thread has been successfully created.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image75.png)

1. Run the cell to create a user message in the conversation thread and display a confirmation message indicating that the message has been successfully sent to Cora.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image76.png)

1. Run the cell to execute the agent, allowing it to process the user message using the file search tool, and display a confirmation message indicating that the agent run has completed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image77.png)

1. Run the cell to retrieve all messages from the conversation thread and display Cora’s response along with the user’s message in a formatted conversation view.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image78.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image79.png)

1. Run the cell to define a helper function that sends a message to Cora, processes it using the agent, and retrieves the assistant’s response from the conversation thread.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image80.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image81.png)

1. Run the cell to test Cora with Paint related questions.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image82.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image83.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image84.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image85.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image86.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image87.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image88.png)


### Task 9: Cora-For-Zava: Building a Multi-Agent Retail Assistant System

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. As Zava retail stores grow, Cora needs to handle more complex customer needs. This notebook shows you how to evolve from a single agent to a multi-agent system, with specialized agents for inventory management and customer service. You'll learn to orchestrate multiple agents working together to provide sophisticated and role-specific assistance.

1. Navigate to the **labs/agents/1-agents** folder and open the **12-agent-framework-orchestration.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image89.png)

1. Click **Select Kernel**, then choose the **Python 3.12.11** environment to run the Lab 02 notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image90.png)

1. Click the **Run (▶)** button to execute the cell and verify that all required Python packages are installed successfully.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image91.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image92.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image93.png)

1. Run the cell to verify your Azure login by creating Azure CLI credentials and confirming that a token is successfully retrieved.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image94.png)

1. Run the cell to connect to the Azure AI Project, retrieve the Azure AI Search connection, and confirm that the project client has been successfully created.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image95.png)

1. Run the cell to define the Product Inventory Agent instructions and display a confirmation message along with the instruction length.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image96.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image97.png)

1. Run the cell to create the Product Inventory Agent with Azure AI Search capabilities and display a confirmation message indicating that the agent has been successfully created.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image98.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image99.png)

1. Run the cell to test the Product Inventory Agent by sending a sample query, processing it with Azure AI Search, and displaying the agent’s response along with relevant citations.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image100.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image101.png)

1. Run the cell to test the Customer Service Agent by sending the same query, processing it with Azure AI Search, and displaying the agent’s response along with relevant citations.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image102.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image103.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image104.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image105.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image106.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image107.png)


### Task 10: Cora-For-Zava: Generating Synthetic Test Datasets for Evaluation

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. To ensure Cora provides accurate and helpful responses about hardware and home improvement products, you need quality test data. This notebook helps you generate synthetic query-response pairs based on your product catalog, creating a robust evaluation dataset to measure Cora's performance before deployment.

1. Navigate to the **labs/2-models/** folder and open the **21-simulated-dataset.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image108.png)

1. Click **Select Kernel**, then choose the **Python 3.12.11** environment to run the Lab 02 notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image109.png)

1. Click **Run All** to execute all the cells in the notebook and observe the outputs.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image110.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image111.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image112.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image113.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image114.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image115.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image116.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image117.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image118.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image119.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image120.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image121.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image122.png)


### Task 11: Cora-For-Zava: Evaluating and Selecting the Best AI Model

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. To ensure Cora provides the best customer experience, you need to select the right foundation model. With multiple Azure OpenAI models available (GPT-4o, GPT-4o-mini, GPT-4), you need to evaluate which model delivers the best balance of quality, safety, and performance for your retail use case.

1. Navigate to the **labs/2-models/** folder and open the **22-evaluate-models.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image123.png)

1. Click **Select Kernel**, then choose the **Python 3.12.11** environment to run the Lab 02 notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image124.png)

1. Click **Run All** to execute all the cells in the notebook and observe the outputs.

    >[!Alert] If you run into any errors regarding GPT model, search for the gpt-4o model, and in the list of models to evaluate, ensure **gpt-4.1** is the only model listed.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image110.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image125.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image126.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image127.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image128.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image129.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image130.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image131.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image132.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image133.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image134.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image135.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image136.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image137.png)


### Task 12: Cora-For-Zava: Getting Started with Your First AI Evaluation Flow

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. Before deploying Cora to help customers, you need to ensure it provides accurate, safe, and helpful responses. Evaluation is the foundation of trust in AI applications, making it a critical part of the Generative AI Ops (GenAIOps) lifecycle. Without rigorous evaluation, Cora could produce content that is fabricated, irrelevant, harmful, or vulnerable to adversarial attacks.

1. Navigate to the **labs/** **4-evaluation/** folder and open the 42-**first-evaluation-run.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image138.png)

1. Click **Select Kernel**, then choose the **Python 3.12.11** environment to run the Lab 02 notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image139.png)

1. Click **Run All** to execute all the cells in the notebook and observe the outputs.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image110.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image140.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image141.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image142.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image143.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image144.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image145.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image146.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image147.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image148.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image149.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image150.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image151.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image152.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image153.png)


### Task 13: Cora-For-Zava: Exploring AI Response Quality Evaluators

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. Cora must provide accurate, relevant, and coherent responses about hardware and home improvement products to Zava customers. This notebook helps you assess response quality using specialized evaluators for groundedness, relevance, coherence, fluency, and similarity—ensuring Cora meets the high standards expected in a production retail environment.

1. Navigate to the **labs/** **4-evaluation/** folder and open the **42-evaluate-quality.ipynb** notebook to begin the environment setup lab.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image154.png)

1. Click **Select Kernel**, then choose the **Python 3.12.11** environment to run the Lab 02 notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image155.png)

1. Click **Run All** to execute all the cells in the notebook and observe the outputs.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image110.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image156.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image157.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image158.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image159.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image160.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image161.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image162.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image163.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image164.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image165.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image166.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image167.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image168.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image169.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image170.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image171.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image172.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image173.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image174.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image175.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image176.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image177.png)


### Task 14: Cora-For-Zava: Exploring AI Safety Evaluators for Secure Responses

**Cora** is a customer service chatbot for **Zava** - a fictitious retailer of home improvement goods for DIY enthusiasts. Before deploying Cora to serve Zava customers, you must ensure it generates safe, appropriate content and is protected against adversarial attacks. This notebook guides you through Azure AI Foundry's safety evaluators, helping you identify and mitigate risks like harmful content, jailbreak attempts, and protected material violations to maintain a secure and trustworthy customer experience.

1. Navigate to the **labs/** **4-evaluation/** folder and open the **43-evaluate-safety.ipynb** notebook to begin the environment setup lab.

1. Click **Select Kernel**, then choose the **Python 3.12.11** environment to run the Lab 02 notebook

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image178.png)

1. Click **Run All** to execute all the cells in the notebook and observe the outputs.

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image110.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image179.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image180.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image181.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image182.png)

    ![](https://raw.githubusercontent.com/technofocus-pte/accagntcaifrntr/refs/heads/main/Spectra-cloudslice/Labguides/Usecase%2009/media/image183.png)


## Summary

In this lab, you implemented a complete **end-to-end AI solution** for a retail assistant using Azure AI Foundry. Starting from environment setup and deployment, you built Cora, enhanced it with search capabilities, and evolved it into a multi-agent system.

You also explored critical aspects of production AI systems, including:
    - Data indexing and retrieval
    - Agent orchestration
    - Model evaluation and selection
    - Safety and quality validation


By the end of this exercise, you gained practical experience in designing, deploying, and managing **scalable, intelligent AI applications** that deliver real-world business value.
