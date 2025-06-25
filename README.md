# Document Assistant with Azure AI Foundry: Building a Custom RAG Solution

## Overview and Architecture

<!-- Placeholder for your architecture diagram image. Replace with your actual image URL -->
<!-- Example: ![Doc Assistant Architecture](https://github.com/your-username/your-repo/assets/your-image-id/doc_assistant_architecture.png ) -->

![azure ai foundry project ](https://github.com/user-attachments/assets/ef17a282-5a4b-4d5b-ace5-6c3e05ca60fd)


### Business Case

In corporate environments, vast amounts of critical information are stored in unstructured documents like PDFs. Traditional Large Language Models (LLMs) often lack access to this proprietary knowledge, leading to generic or inaccurate responses. This project addresses this by building a "Document Assistant" – a Retrieval Augmented Generation (RAG) application – that answers user questions based *only* on provided documents, ensuring accuracy and relevance for internal use cases like legal queries, medical information, or custom support.

### Architecture Overview

This solution leverages Microsoft Azure's comprehensive AI ecosystem to create a robust and scalable RAG application.

1.  **Azure AI Foundry (formerly Azure AI Studio)**: The central platform for managing AI projects, model deployments, and data indexing.
2.  **Azure OpenAI Service**: Provides access to powerful LLMs (e.g., GPT-3.5 Turbo) and embedding models.
3.  **Azure AI Search**: Powers the semantic search and indexing of documents.
4.  **Azure Storage Account**: Stores the raw PDF documents.
5.  **Prompt Flow**: Orchestrates the RAG process, defining the logic for retrieving relevant document chunks and generating responses.
6.  **Endpoint Deployment**: Exposes the RAG solution as a callable API.
7.  **Copilot Studio (formerly Power Virtual Agents)**: Serves as the user-facing conversational interface.
8.  **Power Automate**: Connects the Copilot to the Prompt Flow endpoint.
9.  **Web Integration**: Embeds the Copilot into demo and custom websites for accessibility.

### Key Concepts

-   **Retrieval Augmented Generation (RAG)**: A technique that enhances LLM responses by retrieving relevant information from a knowledge base (your documents) before generating an answer. This prevents hallucination and grounds responses in factual data.
-   **Embedding Models**: Convert text into numerical vectors, allowing for semantic similarity searches.
-   **Large Language Models (LLMs)**: Generate human-like text responses based on the retrieved context.

### Key Benefits

-   **Contextual Accuracy**: Answers are directly derived from provided documents, ensuring high accuracy and trustworthiness.
-   **No Need for Multiple Roles**: Microsoft's integrated tools allow a single individual to manage the entire process.
-   **Widespread Adoption**: Built on Microsoft infrastructure, increasing integration possibilities and career opportunities.
-   **Ease of Use**: User-friendly tools simplify implementation and management.
-   **Clear & Simple Steps**: The development process is structured and easy to follow for both beginners and experts.

---

## Step-by-Step Implementation

### Step 1: Create Azure Resource Group

1.  Open Azure Portal and create a new **Resource Group** to organize all project resources.

---

### Step 2: Create Azure AI Foundry (Azure AI Studio)

1.  Search for and create **Azure AI Studio** (now known as Azure AI Foundry).
2.  During creation, it will automatically provision an **Azure AI Service** and a **Storage Account**.
3.  Launch Azure AI Studio and create a new **Project** within it.

---

### Step 3: Create Azure AI Search

1.  In the same Resource Group, create a new **Azure AI Search** resource.
2.  Select the appropriate pricing tier (Standard recommended for production, Free/Basic for testing if available).

---

### Step 4: Model Deployment

1.  Navigate to your Azure AI Studio project.
2.  Deploy the following models from Azure OpenAI:
    -   **Embedding Model**: `text-embedding-ada-002`
    -   **Large Language Model (LLM)**: `gpt-35-turbo-16k` (or GPT-4 if available and desired)

---

### Step 5: Add Data

1.  In Azure AI Studio, go to the "Data Index" tab.
2.  Upload your PDF documents (e.g., `hotel_info.pdf`) to the associated Storage Account.

---

### Step 6: Create Index

1.  In Azure AI Studio, navigate to the "Index" tab.
2.  Create a new index:
    -   Select the data you uploaded in Step 5.
    -   Choose your **Azure AI Search** resource.
    -   Select your **Azure OpenAI** connection (for embeddings).
    -   Ensure "Create Vector Index" is selected.

---

### Step 7: Playground - Test Model Response

1.  Go to the "Playground" tab in Azure AI Studio.
2.  Select the deployed LLM.
3.  Add your data by selecting the index created in Step 6.
4.  **Crucially, select "Hybrid" as the search type.**
5.  Test with questions related to your documents (e.g., "Where can I stay in New York?"). Verify correct, document-grounded answers.

---

### Step 8: Prompt Flow Setup

1.  Go to the "Prompt Flow" tab in Azure AI Studio.
2.  Create a new flow by cloning the "Multi-round Q&A on your data" sample.
3.  **Enable Managed Identity**:
    -   Go to your Azure AI Studio resource in the Azure Portal.
    -   Under "Identity", enable the **System-assigned managed identity**.
    -   Go to your Storage Account resource.
    -   Under "Access Control (IAM)", add a role assignment: assign the "Storage Blob Data Reader" role to your Azure AI Studio's managed identity. This resolves permission errors for Prompt Flow.
4.  Configure the Prompt Flow:
    -   Start a compute session.
    -   In the "lookup_rectangular_box" node, select your registered index.
    -   In the "chat_with_context" node, select your OpenAI connection and deployed LLM.
    -   Set query type to "Hybrid".
5.  Test the Prompt Flow using the chat icon in the top right corner.

---

### Step 9: Prompt Flow Deployment

1.  Once the Prompt Flow is tested, click "Deploy" from the Prompt Flow interface.
2.  Provide a name for the endpoint and keep default settings (Key authentication).

---

### Step 10: Endpoint Testing (Postman)

1.  Retrieve the **Endpoint URL** and **API Key** from the deployed Prompt Flow endpoint details in Azure AI Studio.
2.  Use **Postman** (or a similar API client) to send a POST request to the endpoint:
    -   Method: `POST`
    -   URL: Your Endpoint URL
    -   Authorization: `Bearer Token` (use your API Key)
    -   Body: `raw` -> `JSON` (e.g., `{"question": "Where can I stay in New York?"}`)
3.  Verify that the correct response is received, confirming the endpoint's functionality.

---

### Step 11: Copilot Studio Integration

1.  Open **Copilot Studio** (formerly Power Virtual Agents).
2.  Create a new **Agent** (Copilot).
3.  Disable the default OpenAI integration.
4.  Create a new **Topic** (e.g., "RAG Topic") with relevant trigger phrases.
5.  Within the topic, integrate with **Power Automate**:
    -   Create a new Power Automate flow.
    -   This flow will receive the user's question from Copilot.
    -   It will then make an **HTTP POST request** to your Prompt Flow endpoint (using the URL and API Key).
    -   Parse the JSON response from the endpoint.
    -   Return the generated answer back to Copilot.
6.  Test the Copilot to ensure it correctly retrieves answers via Power Automate.

---

### Step 12: Copilot Integration with Websites

1.  In Copilot Studio, go to "Settings" -> "Security" -> "Authentication" and select "No authentication" for demo purposes.
2.  Publish your Copilot.
3.  Integrate with a **Demo Website**: Copy the provided demo website link from Copilot Studio and test.
4.  Integrate with a **Custom Website**: Copy the embed code from Copilot Studio and paste it into your website's source code.

---

## Key Considerations

-   **Security**: For production environments, implement robust authentication and authorization for endpoints and data access.
-   **Cost Optimization**: Monitor resource consumption (especially LLM tokens and compute sessions) to manage costs.
-   **Scalability**: Design for scalability by choosing appropriate Azure service tiers and managing concurrent requests.
-   **Document Management**: Establish a clear process for updating and re-indexing documents as your knowledge base evolves.
-   **Prompt Engineering**: Fine-tune Prompt Flow configurations and system prompts for optimal response quality.

This project provides a comprehensive guide to building a custom RAG-based Document Assistant using Microsoft Azure AI Foundry, demonstrating a powerful application of generative AI for enterprise knowledge retrieval.


![1](https://github.com/user-attachments/assets/a56bd908-1fb7-4007-b702-f32ad12897ef)

![2](https://github.com/user-attachments/assets/019efe51-a304-4df7-aba6-99ae60d38214)

![5](https://github.com/user-attachments/assets/72b7c3d3-685e-4281-9e97-5570ac033c4d)

![7](https://github.com/user-attachments/assets/11bb9588-dcc5-42e6-b278-6d320dfa6dab)

![8](https://github.com/user-attachments/assets/df4d668e-07d7-4e9a-9216-f05237f8cd63)

![9](https://github.com/user-attachments/assets/2c9d4400-05e6-4403-930d-412a0f9f05ad)

![10](https://github.com/user-attachments/assets/0f437c9f-f6d4-4664-ba5a-f9a13818414a)



