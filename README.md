Gerne, hier sind die kürzeren und umstrukturierten Texte für dein Projektportfolio und dein GitHub README-File.

---

## Text für dein Projektportfolio (Kürzere Version)

**Project: Document Assistant with Azure AI Foundry (RAG Application)**

**Project Overview**

In Unternehmen fallen riesige Mengen unstrukturierter Daten in Form von PDFs und Dokumenten an. Herkömmliche Large Language Models (LLMs) können diese internen Informationen nicht nutzen, was zu ineffizienter Informationsbeschaffung und ungenauen Antworten führt. Dieses Projekt löst dieses Problem durch die Entwicklung eines "Dokumenten-Assistenten" – einer Retrieval Augmented Generation (RAG)-Anwendung. Dieser Assistent beantwortet Fragen ausschließlich auf Basis bereitgestellter Dokumente, um präzise und kontextbezogene Antworten zu liefern, ohne sich auf das allgemeine Wissen des LLM zu verlassen.

**Key Metrics (KPIs)**

*   **Answer Accuracy:** Percentage of correct, document-supported responses.
*   **Response Time:** Time taken to generate an answer.
*   **User Satisfaction:** Feedback on usefulness and ease of use.
*   **Document Coverage:** Breadth of information retrievable.
*   **Cost Efficiency:** Optimization of Azure resource consumption.

**Project Goals & Outcomes**

Das Hauptziel war der Aufbau eines zuverlässigen, dokumentenbasierten Frage-Antwort-Systems. Wir haben eine End-to-End RAG-Anwendung mit Microsoft Azure AI Foundry entwickelt, die fortschrittliche KI-Lösungen in einer robusten Cloud-Umgebung demonstriert. Durch die Automatisierung des Q&A-Endpoints mittels Prompt Flow und die Integration in einen benutzerdefinierten Copilot wurde eine nahtlose und intuitive Benutzererfahrung geschaffen.

**Key Achievements:**

*   **Kontextuelle Genauigkeit:** Antworten werden direkt aus den Dokumenten abgeleitet, was die Vertrauenswürdigkeit erheblich steigert.
*   **Skalierbare Lösung:** Nutzung von Azure-Diensten für eine robuste und skalierbare Infrastruktur.
*   **Vereinfachte KI-Entwicklung:** Azure AI Foundry optimiert die Bereitstellung und Verwaltung von KI-Modellen.
*   **Vielseitige Anwendung:** Das Framework ist anpassbar für spezialisierte Assistenten in verschiedenen Branchen.
*   **Nahtlose Integration:** Die Anbindung an Copilot Studio und Power Automate ermöglicht die Einbettung in bestehende Workflows.

**What was done:**

Dieses Projekt umfasste die umfassende Entwicklung und Bereitstellung eines Dokumenten-Assistenten (RAG-Anwendung) auf Microsoft Azure:

1.  **Azure Ressourcenbereitstellung:** Erstellung einer dedizierten Ressourcengruppe, Bereitstellung von Azure AI Foundry (inkl. Azure AI Service und Storage Account) und Azure AI Search.
2.  **Modell-Deployment:** Bereitstellung eines Embedding-Modells (`text-embedding-ada-002`) und eines Large Language Models (`gpt-35-turbo-16k`) aus Azure OpenAI.
3.  **Daten-Ingestion & Indexierung:** Hochladen von PDF-Dokumenten und Erstellung eines Suchindex in Azure AI Search.
4.  **Modell-Testing:** Überprüfung der Modellantworten im Azure AI Foundry Playground.
5.  **Prompt Flow Entwicklung & Deployment:** Erstellung eines Prompt Flows zur Orchestrierung der RAG-Anwendung, Behebung von Berechtigungsproblemen (Managed Identity) und Deployment als sicherer Endpoint.
6.  **Endpoint-Testing:** Verifizierung der Endpoint-Funktionalität mittels Postman.
7.  **Copilot-Integration:** Aufbau eines benutzerdefinierten Copilots (Power Virtual Agent) in Copilot Studio, Integration über Power Automate und Anbindung an Demo- und benutzerdefinierte Websites.

---

## GitHub README-File Text (Kürzere Version)

```markdown
# Document Assistant with Azure AI Foundry: Building a Custom RAG Solution

## Overview and Architecture

<!-- Placeholder for your architecture diagram image. Replace with your actual image URL -->
<!-- Example: ![Doc Assistant Architecture](https://github.com/your-username/your-repo/assets/your-image-id/doc_assistant_architecture.png) -->
![Doc Assistant Architecture Diagram Placeholder](https://via.placeholder.com/800x400?text=Doc+Assistant+Architecture+Diagram)

### Business Context

Organizations often struggle to extract specific information from vast amounts of unstructured internal documents. Traditional LLMs lack this proprietary knowledge, leading to generic or inaccurate responses. This project tackles this by developing a "Document Assistant" – a Retrieval Augmented Generation (RAG) application – that answers user questions *only* based on provided documents, ensuring accuracy and relevance for internal use cases.

### Key Components

This solution leverages Microsoft Azure's comprehensive AI ecosystem:

1.  **Azure AI Foundry (formerly Azure AI Studio)**: Central platform for AI project management.
2.  **Azure OpenAI Service**: Provides LLMs and embedding models.
3.  **Azure AI Search**: Powers document indexing and retrieval.
4.  **Azure Storage Account**: Stores raw documents.
5.  **Prompt Flow**: Orchestrates the RAG process.
6.  **Endpoint Deployment**: Exposes the RAG solution as an API.
7.  **Copilot Studio (formerly Power Virtual Agents)**: User-facing conversational interface.
8.  **Power Automate**: Connects Copilot to the Prompt Flow endpoint.
9.  **Web Integration**: Embeds the Copilot into websites for accessibility.

### Key Benefits

-   **Contextual Accuracy**: Answers are directly derived from provided documents.
-   **Simplified Development**: Microsoft's integrated tools streamline the process.
-   **Scalability**: Built on Azure for robust and scalable infrastructure.
-   **Versatility**: Adaptable for various industry-specific assistants.

---

## Step-by-Step Implementation

### 1. Azure Resource Setup

-   Create a **Resource Group**.
-   Provision **Azure AI Foundry** (auto-creates AI Service & Storage Account).
-   Create **Azure AI Search** resource.

---

### 2. Model Deployment

-   Deploy **Embedding Model** (`text-embedding-ada-002`) and **LLM** (`gpt-35-turbo-16k`) from Azure OpenAI within AI Foundry.

---

### 3. Data Ingestion & Indexing

-   Upload PDF documents to AI Foundry.
-   Create a **Search Index** in Azure AI Search, linking documents to the embedding model.

---

### 4. Model Testing (Playground)

-   Test the integrated LLM and search index in the AI Foundry Playground, using "Hybrid" search.

---

### 5. Prompt Flow Development & Deployment

-   Clone "Multi-round Q&A" sample flow.
-   **Enable Managed Identity** for AI Studio and grant "Storage Blob Data Reader" role to resolve permissions.
-   Configure flow nodes (index, LLM connection).
-   Deploy the Prompt Flow as a secure **endpoint**.

---

### 6. Endpoint Testing

-   Retrieve Endpoint URL and API Key.
-   Test functionality using **Postman** to send POST requests.

---

### 7. Copilot Studio Integration

-   Create a custom **Copilot** in Copilot Studio.
-   Build a **Power Automate flow** to connect Copilot to the Prompt Flow endpoint (HTTP POST request).
-   Integrate Copilot with a **demo website** and a **custom website**.

---

## Key Considerations

-   **Security**: Implement robust authentication for production.
-   **Cost Optimization**: Monitor resource consumption.
-   **Scalability**: Choose appropriate Azure service tiers.
-   **Prompt Engineering**: Fine-tune configurations for optimal response quality.

This project demonstrates building a custom RAG-based Document Assistant using Microsoft Azure AI Foundry, showcasing a powerful application of generative AI for enterprise knowledge retrieval.
```
