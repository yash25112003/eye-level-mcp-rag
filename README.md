# GroundX RAG Assistant

**Smart Document Q&A and Ingestion.**

The GroundX RAG Assistant is an AI-powered system designed to facilitate intelligent question-answering over a custom knowledge base and enable seamless document ingestion. By leveraging GroundX for content search and retrieval, and exposing these functionalities as tools via FastMCP, it provides a robust framework for RAG (Retrieval Augmented Generation) applications.

## 🌟 Features

* **Intelligent Document Search:** Retrieves highly relevant context from a GroundX knowledge base based on user queries, supporting accurate AI responses.
* **Effortless Document Ingestion:** Allows for easy upload and integration of local PDF documents into the knowledge base, making them immediately available for search.
* **Tool-Based Architecture:** Exposes core functionalities as discrete tools via FastMCP, enabling flexible integration into larger AI agent systems or interactive console applications.
* **Scalable Knowledge Base:** Utilizes GroundX as the underlying platform for managing and searching a vast collection of documents.

## 🛠️ Technical Implementation

### 🔍 Core Technologies

* **Python**: The primary programming language.
* **GroundX SDK**: Official Python SDK for interacting with the GroundX platform for document management and search.
* **FastMCP**: A framework for creating and exposing tools that can be consumed by AI models or other applications, simplifying complex interactions.
* **`python-dotenv`**: For secure management of environment variables (e.g., API keys).

### 📂 Project Structure

```bash
groundx-rag-assistant/
├── main.py               # Main script defining and exposing GroundX tools via FastMCP
├── .env                  # Environment variables for API keys
└── requirements.txt      # Python dependencies
```

## 🚀 Getting Started

Follow these steps to set up and run the GroundX RAG Assistant on your local machine.

### Prerequisites

* Python 3.8+
* `pip` package manager
* A GroundX account with a configured `bucket_id` (e.g., `17279` from your code) and `id` (e.g., `17221` from your code) for content searching.

### Installation

1.  **Clone the repository:**

    ```bash
    git clone <your-repository-url>
    cd groundx-rag-assistant
    ```

    *(Note: Replace `<your-repository-url>` with your actual repository URL.)*

2.  **Create and activate a virtual environment:**

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
    ```

3.  **Install Dependencies:**
    Create a `requirements.txt` file in your project root with the following content:

    ```
    groundx
    fastmcp
    python-dotenv
    ```

    Then, install them:

    ```bash
    pip install -r requirements.txt
    ```

### Configuration

1.  **Environment Variables (`.env` file):**
    Create a file named `.env` in the root of your project:

    ```env
    GROUNDX_API_KEY="YOUR_GROUNDX_API_KEY"
    ```

    * **`GROUNDX_API_KEY`**: Obtain your API key from your GroundX account settings.

## 🖥️ Usage Guide

The `main.py` script starts a FastMCP server that exposes the `search_doc_for_rag_context` and `ingest_documents` tools via standard I/O (stdio). You can interact with it programmatically or via a console.

To run the application:

```bash
source venv/bin/activate # Activate your virtual environment
python main.py
```

Once running, the `FastMCP` server will be active. You can then call its tools.

### Example Tool Usage (Conceptual):

To use these tools, another process (e.g., an LLM agent, a chatbot interface, or a testing script) would typically communicate with this `FastMCP` server over `stdio`.

**1. Searching for RAG Context:**

A tool call to `search_doc_for_rag_context` would look like this (from the perspective of the calling system):

```json
{
  "tool_name": "search_doc_for_rag_context",
  "args": {
    "query": "What are the benefits of a balanced diet for children?"
  }
}
```

The server would then return the relevant context from GroundX.

**2. Ingesting Documents:**

A tool call to `ingest_documents` would look like this:

```json
{
  "tool_name": "ingest_documents",
  "args": {
    "local_file_path": "/path/to/your/document.pdf"
  }
}
```

The server would confirm the ingestion process.

*(Note: The actual interaction mechanism depends on how `FastMCP`'s `stdio` transport is integrated with the calling application.)*
