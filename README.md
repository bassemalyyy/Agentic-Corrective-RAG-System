# Agentic-Corrective-RAG-System
This project will cover a full hands-on workflow and demonstration of how to build an Agentic Corrective RAG (CRAG) System with LangGraph, it's adapted from [Analytics Vidhya](https://courses.analyticsvidhya.com/courses/take/building-an-agentic-corrective-rag-system-in-langgraph/lessons/61962780-building-an-agentic-corrective-rag-system) free courses.

# Overview

The Agentic CRAG system enhances traditional RAG by incorporating checks for document relevance and performing web searches when retrieved documents are insufficient. The system is structured as a graph where each node represents a specific functionality, orchestrated using LangGraph. 

## Key steps include:

- Retrieval from Vector Database: Fetch relevant documents based on the user query.



- Document Relevance Check: Evaluate whether retrieved documents are relevant to the query.



- Query Rewriting and Web Search: If documents are not relevant, rewrite the query and perform a web search to gather additional context.



- Response Generation: Generate accurate answers using the retrieved or augmented context.

The system is designed to mitigate issues like poor retrieval and out-of-context or hallucinated answers by dynamically adjusting its workflow.

## Features

- Agentic Workflow: Utilizes LangGraph to create a flexible, node-based workflow.

- Relevance Checking: Assesses the relevance of retrieved documents to ensure high-quality responses.

- Web Search Integration: Augments context with web searches when vector database results are inadequate.

- LLM Integration: Leverages local Ollama LLM models (**gemma3n:e4b** and **llama3.2**) and the **nomic-embed-text** embedding model for query processing and response generation.

## Installation

To set up the project, follow these steps:

**1- Clone the Repository:**
```sh
git clone https://github.com/bassemalyyy/agentic-crag-system.git
```

**2- Install Dependencies:** Ensure you have Python 3.10 or higher installed. Then, install the required packages:

```sh
pip install langchain langchain-ollama langchain-community langgraph
```
The **corrective-rag-system.ipynb** notebook includes the full dependency installation commands, which are already satisfied in the provided environment:
- langchain
- langchain-groq
- langchain-community
- langgraph

**3- Set Up Environment:**

- Install and configure Ollama to run the local LLM models (**gemma3n:e4b** and **llama3.2**) and the embedding model (**nomic-embed-text**).

```sh
ollama pull gemma3n:e4b
ollama pull llama3.2
ollama pull nomic-embed-text
```


- Ensure Ollama is running locally:

```sh
ollama run
```


- Ensure you have access to a vector database and configure it as needed.

- Get you free [Tavily API key](https://app.tavily.com/home), in the third cell of the code enter your API Key:

```sh
from getpass import getpass

TAVILY_API_KEY = getpass('Enter Tavily Search API Key: ')
```


- Run the Notebook: Open the corrective-rag-system.ipynb notebook in Jupyter or a compatible environment (e.g., VS Code, Colab) and execute the code.

## Usage

The notebook demonstrates the Agentic CRAG system with example queries. To test the system:

**1- Open the Notebook:** Load corrective-rag-system.ipynb in a Jupyter environment.

**2- Run the Cells:**

- Execute the dependency installation cell to ensure all packages are available.



- Run the cell that displays the LangGraph workflow diagram to visualize the system.

- Test the system with provided queries like:

  - ``what is an agent?``
  - ``what is CrewAI agent?``
  - ``what is orchestration?``


**3- Example Queries:** The notebook includes example queries and their responses:


   - **Query:** `"what is an agent?"`  
     - **Response:** Describes an agent as a system that independently accomplishes tasks using an LLM, with capabilities for workflow management and tool access. -> **THIS RESPONSE IS RETRIEVED FROM THE DOCUMENTS AS THE QUERY IS RELEVANT TO THE DOCUMENTS**

   - **Query:** `"what is CrewAI agent?"`  
     - **Response:** Explains a CrewAI agent as an autonomous unit within the CrewAI framework, capable of task execution, decision-making, and collaboration. -> **THIS RESPONSE IS RETRIEVED FROM THE WEB SEARCH RESULTS AS THE QUERY IS NOT RELEVANT TO THE DOCUMENTS**

   - **Query:** `"what is orchestration?"`  
     - **Response:** Defines orchestration as managing workflow execution in single or multi-agent systems, including patterns like the manager pattern. -> **THIS RESPONSE IS RETRIEVED FROM THE DOCUMENTS AS THE QUERY IS RELEVANT TO THE DOCUMENTS**


**4- Custom Queries:** Modify the query variable in the notebook to test custom questions. For example:

```sh
query = "your custom question here"
response = agentic_rag.invoke({"question": query})
display(Markdown(response['generation']))
```

## Project Structure

- **corrective-rag-system.ipynb**: The main Jupyter notebook containing the implementation and test cases.

- **README.md**: This file, providing an overview and instructions for the project.

## Workflow Diagram

The system’s workflow is visualized using a LangGraph-generated diagram, as shown below:

![CRAG-Diagram](https://github.com/user-attachments/assets/d31ab69c-80fb-4fe9-bb59-3f5d26b5bc4c)

This diagram illustrates the nodes and decision points in the CRAG system, including retrieval, relevance checking, query rewriting, web search, and response generation.

## Notes


- **Environment:** The notebook was tested in a Python 3.10 environment with the specified dependencies.

- **Local Models:** The system uses local Ollama models (**gemma3:e4b**, **llama3.2**, and **nomic-embed-text**).

- **Vector Database:** The system assumes access to a vector database for document retrieval. Configure your database connection as needed.

- **Extensibility:** The system can be extended by adding new nodes to the LangGraph workflow or integrating additional tools for web search or document processing.
