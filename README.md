# [AI for Bharat] Context-Aware RAG Application using Amazon Bedrock

💡 Project Overview
This project implements a Retrieval-Augmented Generation (RAG) application designed to provide accurate, grounded answers to user questions based only on proprietary or domain-specific documents. It solves the common challenge of LLM hallucinations by linking a powerful Foundation Model (FM) to a trusted knowledge base.

✨ Key Features
Grounded Responses: Answers are retrieved from a secure knowledge base, ensuring factual accuracy and eliminating common LLM errors.

Semantic Search: Utilizes vector embeddings for semantic search, finding relevant content even when keywords don't match exactly.

AWS Integration: Built entirely using modern serverless and managed services, providing a robust and scalable architecture.

Intuitive Interface: Features a simple web interface built with Streamlit for easy interaction.

🏛️ Architecture
The solution follows the standard RAG pattern, leveraging Knowledge Bases for Amazon Bedrock to orchestrate the entire workflow.


![Nano-service architecture diagram]("C:\Users\hp\OneDrive\Desktop\licensed-image.jpg")




1 Ingestion: Proprietary documents are loaded into the Knowledge Base.

2 Embedding & Storage: Amazon Bedrock chunks the documents, generates vector embeddings, and stores them in Amazon OpenSearch Serverless (the Vector Store).

3 Query: A user submits a query via the Streamlit interface.

4 Retrieval: The query is routed to the Knowledge Base, which queries the OpenSearch Vector Store to fetch the most relevant text chunks.

5 Generation: The original query and the retrieved context chunks are combined into a prompt and sent to the selected Amazon Bedrock Foundation Model (e.g., Anthropic Claude).

6 Response: The LLM generates the final answer based only on the provided context, which is then displayed to the user.


⚙️ Services Used
Service,Role in Project
Amazon Bedrock,"Provides access to the LLMs (FM) for generation (e.g., Claude 3 Sonnet)."
Knowledge Bases for Amazon Bedrock,"Manages the RAG pipeline; handles chunking, embedding, retrieval, and prompt construction."
Amazon OpenSearch Serverless,Serves as the scalable vector database (Vector Store) for semantic search.
AWS SDK (Boto3),Used for programmatic interaction with AWS services.
Streamlit,The Python framework used for creating the frontend chat interface.


🛠️ Getting Started
Prerequisites
AWS Account with necessary permissions for Bedrock, OpenSearch, and IAM.

Python 3.9+

The boto3 and streamlit Python libraries.


Installation & Setup

Clone the Repository:

Bash
git clone [YOUR GITHUB LINK]
cd [repository-name]
Install Dependencies:

Bash
pip install -r requirements.txt
Configure AWS Credentials: Ensure your local AWS CLI credentials are set up with access to the Bedrock service region.


Run the Application:
Bash
streamlit run app.py

📧 Contact
For questions or feedback, please reach out to Sudarshanam Yessasvini at yessasvini.s@gmail.com.

