---
page_type: sample
languages:
- csharp
products:
- azure-cosmos-db
- azure-openai
name: Sample chat app using Azure Cosmos DB for NoSQL and Azure OpenAI
urlFragment: chat-app
description: Sample application that implements multiple chat threads using the Azure OpenAI "text-davinci-003" model and Azure Cosmos DB for NoSQL for storage.
azureDeploy: https://raw.githubusercontent.com/azure-samples/cosmosdb-chatgpt/main/azuredeploy.json
---

# Azure Cosmos DB + OpenAI ChatGPT

此示例應用程序將Azure Cosmos DB與OpenAI ChatGPT結合，並使用Blazor Server前端，打造一個智能聊天機器人應用程式，展示如何利用OpenAI ChatGPT和Azure Cosmos DB構建一個簡單的聊天應用程式。

![Cosmos DB + ChatGPT user interface](screenshot.png)

## Features

此應用程式有個別的聊天會話，可以在左側導航中顯示和選擇。點擊一個會話將顯示包含人類提示和AI完成的消息。

當向Azure OpenAI服務發送新提示時，會將部分對話歷史記錄一起發送。這提供了上下文，使ChatGPT能夠像在進行對話一樣回應。這個對話歷史記錄的長度可以從appsettings.json中進行配置，使用OpenAiMaxTokens值，然後將其轉換為最大對話字符串長度的1/2。

請注意，此示例使用的"text-davinci-003"模型最多只能使用4096個令牌。令牌在服務的請求和響應中都會使用。將maxConversationLength覆蓋為接近最大令牌值的值可能會導致完成只包含很少或沒有文本，如果所有文本都在請求中使用。

每個聊天會話的所有提示和完成的歷史記錄都存儲在Azure Cosmos DB中。在UI中刪除聊天會話將同時刪除其對應的數據。

應用程序還將通過要求ChatGPT提供第一個提示的一個或兩個字的摘要來總結聊天會話的名稱。這使您可以輕鬆識別不同的聊天會話。

請注意，這是一個示例應用程序。它旨在演示如何將Azure Cosmos DB和Azure OpenAI ChatGPT一起使用。它不適用於生產或其他大規模使用。


## Getting Started

### Prerequisites

- Azure Subscription
- Subscription access to Azure OpenAI service. Start here to [Request Acces to Azure OpenAI Service](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUOFA5Qk1UWDRBMjg0WFhPMkIzTzhKQ1dWNyQlQCN0PWcu)
- Visual Studio, VS Code, or some editor if you want to edit or view the source for this sample.


### Installation

1. Fork this repository to your own GitHub account.
1. Depending on whether you deploy using the ARM Template or Bicep, modify this variable in one of those files to point to your fork of this repository, "webSiteRepository": "https://github.com/Azure-Samples/cosmosdb-chatgpt.git" 
1. If using the Deploy to Azure button below, also modify this README.md file to change the path for the Deploy To Azure button to your local repository.
1. If you deploy this application without making either of these changes, you can update the repository by disconnecting and connecting an external git repository pointing to your fork.


The provided ARM or Bicep Template will provision the following resources:
1. Azure Cosmos DB account with database and container at 400 RU/s. This can optionally be configured to run on the Cosmos DB free tier if available for your subscription.
1. Azure App service. This will be configured for CI/CD to your forked GitHub repository. This service can also be configured to run on App Service free tier.
1. Azure Open AI account. You must also specify a name for the deployment of the "text-davinci-003" model which is used by this application.

Note: You must have access to Azure Open AI service from your subscription before attempting to deploy this application.

All connection information for Azure Cosmos DB and Open AI is zero-touch and injected as environment variables in the Azure App Service instance at deployment time. 

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fcosmosdb-chatgpt%2Fmain%2Fazuredeploy.json)


### Quickstart

1. After deployment, go to the resource group for your deployment and open the Azure App Service in the Azure Portal. Click the web url to launch the website.
1. Click + New Chat to create a new chat session.
1. Type your question in the text box and press Enter.


## Clean up

To remove all the resources used by this sample, you must first manually delete the deployed model within the Azure AI service. You can then delete the resource group for your deployment. This will delete all remaining resources.

## Resources

- [Azure Cosmos DB + Azure OpenAI ChatGPT Blog Post Announcement](https://devblogs.microsoft.com/cosmosdb/)
- [Azure Cosmos DB Free Trial](https://aka.ms/TryCosmos)
- [Open AI Platform documentation](https://platform.openai.com/docs/introduction/overview)
- [Azure Open AI Service documentation](https://learn.microsoft.com/azure/cognitive-services/openai/)
