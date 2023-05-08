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

- Azure 訂用帳戶
- 訂閱訪問 Azure OpenAI 服務。 從[Azure OpenAI 服務](https://customervoice.microsoft.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR7en2Ais5pxKtso_Pz4b1_xUOFA5Qk1UWDRBMjg0WFhPMkIzTzhKQ1dWNyQlQCN0PWcu)請求訪問
- 如果要編輯或查看此示例的源代碼，請使用 Visual Studio、VS Code 或某些編輯器。


### Installation

1. 將此存儲庫fork到您自己的GitHub帳戶中。
1. 根據您是使用ARM模板還是Bicep，修改其中一個文件中的此變量，以指向您的存儲庫的fork，"webSiteRepository": "https://github.com/Azure-Samples/cosmosdb-chatgpt.git" 
1. 如果使用下面的“部署到Azure”按鈕進行部署，還要修改此README.md文件，以將“部署到Azure”按鈕的路徑更改為您的本地存儲庫。
1. 如果您在不進行這些更改的情況下部署此應用程序，則可以通過斷開並連接指向您的fork的外部git存儲庫來更新存儲庫。


提供的ARM或Bicep模板將提供以下資源：
1. Azure Cosmos DB帳戶，其中包含400 RU / s的數據庫和容器。如果您的訂閱可用，還可以將其配置為在Cosmos DB免費層上運行。
1. Azure應用服務。這將被配置為CI / CD到您forked的GitHub存儲庫。此服務也可以配置為在應用服務免費層上運行。
1. Azure Open AI帳戶。您還必須為此應用程序使用的“text-davinci-003”模型的部署指定一個名稱。

注意：在嘗試部署此應用程序之前，您必須從訂閱中訪問Azure Open AI服務。

Azure Cosmos DB和Open AI的所有連接信息都是零觸摸的，並在部署時作為環境變量注入到Azure App Service實例中。 

[![部署到Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure-Samples%2Fcosmosdb-chatgpt%2Fmain%2Fazuredeploy.json)


### Quickstart

1. 部署後，轉到您的部署的資源群組，並在Azure門戶中打開Azure應用服務。單擊Web URL以啟動網站。
1. 點擊+ New Chat以創建一個新的聊天會話。
1. 在文本框中輸入您的問題，然後按Enter鍵。


## Clean up

要刪除此示例使用的所有資源，您必須先手動刪除Azure AI服務中部署的模型。然後，您可以刪除您的部署的資源群組。這將刪除所有剩餘的資源。

## Resources

- [Azure Cosmos DB + Azure OpenAI ChatGPT Blog Post Announcement](https://devblogs.microsoft.com/cosmosdb/)
- [Azure Cosmos DB Free Trial](https://aka.ms/TryCosmos)
- [Open AI Platform documentation](https://platform.openai.com/docs/introduction/overview)
- [Azure Open AI Service documentation](https://learn.microsoft.com/azure/cognitive-services/openai/)
