
# 🤖 AI-Powered Document Chatbot

An intelligent chatbot designed to understand and answer questions based on a private knowledge base of documents. This project leverages the power of Large Language Models (LLMs) and automation workflows to create a seamless Retrieval-Augmented Generation (RAG) system.

## 🌟 Overview

This chatbot automates the process of ingesting documents, processing their content, and providing accurate, context-aware answers to user queries. Simply drop a file into a designated Google Drive folder, and an n8n workflow automatically handles the rest—from text extraction and chunking to vector embedding and storage. The system then uses this knowledge base to answer questions with the help of Google's Gemini model.

## ✨ Key Features

-   **Automated Document Ingestion**: Triggers automatically when new files (PDF, TXT, etc.) are added to a Google Drive folder.
-   **Intelligent Text Processing**: Smartly chunks large documents and creates overlapping text segments to preserve semantic context.
-   **Vector-Based Retrieval**: Uses Pinecone to store document embeddings for fast and accurate similarity searches.
-   **Advanced Q&A**: Leverages the Google Gemini LLM via LangChain to generate human-like, accurate answers based on the retrieved context.
-   **Workflow-Driven**: Built entirely on [n8n](https://n8n.io/), allowing for easy visualization and modification of the entire process.

## 🛠️ Tech Stack

This project is built with a modern, powerful stack:

-   **Automation Workflow**: [n8n.io](https://n8n.io/)
-   **LLM Framework**: [LangChain](https://www.langchain.com/)
-   **Language Model**: [Google Gemini](https://deepmind.google/technologies/gemini/)
-   **Vector Database**: [Pinecone](https://www.pinecone.io/)
-   **Programming Language**: Python & JavaScript (for custom code nodes in n8n)
-   **File Storage**: Google Drive

## ⚙️ System Architecture

The chatbot operates on an event-driven n8n workflow:

1.  **Trigger**: A `Google Drive Trigger` node watches for new files in a specific folder.
2.  **File Processing**: The workflow downloads the file and uses a `Switch` node to route it based on its type (PDF, TXT).
3.  **Text Extraction**: Text is extracted from the document.
4.  **Chunking**: The extracted text is passed to a `Text Splitter` node, which breaks it down into small, overlapping chunks to maintain context.
5.  **Embedding & Storage**: Each chunk is converted into a vector embedding and stored in a Pinecone index along with its metadata.
6.  **Question Answering**: When a user asks a question, a separate workflow (or a webhook trigger) takes the query, creates an embedding, and searches Pinecone for the most relevant document chunks.
7.  **Response Generation**: The user's query and the retrieved chunks are passed to the Gemini LLM via a `LangChain` node, which generates a final, coherent answer.

## 🚀 Getting Started

### Prerequisites

-   An n8n instance (Cloud or self-hosted)
-   Accounts for Google Drive, Pinecone, and Google AI Studio (for API keys)
-   Node.js installed (if running n8n locally)

### Installation & Setup

1.  **Clone the Repository**
    ```sh
    git clone [https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git](https://github.com/YOUR_USERNAME/YOUR_REPO_NAME.git)
    ```
2.  **Import the n8n Workflow**
    -   In your n8n canvas, select "Import from File" and upload the `.json` workflow file from this repository.
3.  **Configure Credentials**
    -   In the n8n sidebar, navigate to "Credentials" and add new credentials for:
        -   Google Drive API
        -   Pinecone API
        -   Google Gemini API
4.  **Set Up Environment Variables**
    -   Update the relevant nodes (e.g., Pinecone, Gemini) to use your newly created credentials.
    -   Specify your Google Drive folder ID and Pinecone index name in the appropriate nodes.
5.  **Activate the Workflow**
    -   Save and activate the workflow. Now you're ready to go!

## 💡 Usage

To start using the chatbot, simply drop a `.pdf` or `.txt` file into the Google Drive folder you configured. The workflow will automatically process and "learn" its contents. You can then use the query part of the workflow to ask questions related to the documents you've uploaded.

**Example Query**: "What were the key findings mentioned in the Q3 report?"

## 🤝 Contributing


<img width="1895" height="908" alt="image" src="https://github.com/user-attachments/assets/e3edcc57-e7ff-4c80-989c-8c28be689b42" />

Contributions are welcome! If you have ideas for improvements or find any issues, please open an issue or submit a pull request.

---
