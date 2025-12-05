
# 🚀 Context-Aware RAG Application on AWS  
*A scalable Retrieval-Augmented Generation (RAG) system using Amazon Bedrock, OpenSearch Serverless, S3 & Lambda*

---

## 📌 Overview  
This project demonstrates how to build a **context-aware AI assistant** using **Retrieval-Augmented Generation (RAG)** on AWS.  
The system ingests domain-specific documents, embeds them using **Amazon Bedrock**, stores them in **OpenSearch Serverless**, and provides contextual answers with significantly reduced hallucinations.

---

## 🧠 Problem Statement  
Organizations struggle to use their internal documents effectively. Traditional LLMs cannot answer domain-specific queries accurately.

**Key challenges:**
- Missing context  
- Hallucinations  
- Lack of traceability  
- Low performance at scale  

---

## 💡 Solution  
A **RAG-powered knowledge assistant** that delivers:
- Context-grounded answers  
- Semantic search across internal data  
- Scalable ingestion and retrieval pipeline  
- Fully serverless deployment on AWS  

---

## 🏗️ Architecture  

![Architecture](./diagrams/architecture.png)

### 🔧 Components
| Component | Service |
|----------|---------|
| Document storage | Amazon S3 |
| Embeddings | Amazon Bedrock (Titan Embed / Sonar Embeddings) |
| Vector Search | OpenSearch Serverless |
| Ingestion logic | AWS Lambda |
| Retrieval logic | AWS Lambda |
| Public interface | Amazon API Gateway |
| Logging & Monitoring | CloudWatch |

---

## ⚙️ How It Works

### **1️⃣ Ingestion Pipeline**
1. Upload a document to **S3**
2. S3 triggers Lambda (`lambda_ingest.py`)
3. Lambda:
   - Cleans text  
   - Chunks documents  
   - Generates embeddings using **Bedrock**  
4. Stores chunks + vectors in **OpenSearch**

---

### **2️⃣ Retrieval Pipeline**
1. User sends question via **API Gateway**
2. Lambda (`lambda_retrieve.py`) generates embedding for query
3. Performs vector similarity search on OpenSearch
4. Sends matched context + query to LLM via **Bedrock**
5. Returns **context-grounded answer**

---

## 📂 Folder Structure  
(Refer to the project tree above.)

---

## 🧩 Code Snippets

### 🟦 Embeddings Example (Bedrock)

```python
response = bedrock.invoke_model(
    modelId="amazon.titan-embed-text-v1",
    body=json.dumps({"inputText": text})
)
embedding = json.loads(response["body"].read())["embedding"]
```

---

### 🟪 OpenSearch Vector Index Creation

```python
index_body = {
  "settings": {"index": {"knn": True}},
  "mappings": {
    "properties": {
      "embedding": {"type": "knn_vector", "dimension": 1536},
      "text": {"type": "text"}
    }
  }
}
```

---

## 🚀 Deployment

### **Option A — CloudFormation**
```
cd infrastructure/cloudformation
aws cloudformation deploy --template-file rag_stack.yaml --stack-name rag-pipeline
```

### **Option B — Terraform**
```
cd infrastructure/terraform
terraform init
terraform apply
```

---

## 📈 Scaling Strategy
- Lambda Provisioned Concurrency  
- OpenSearch Serverless scaling policies  
- S3 multi-region replication  
- Add caching layer via ElastiCache  
- Use Kinesis for high-volume document ingestion  

Read more:  
📄 `docs/scaling_strategy.md`

---

## 🧪 Testing  
Local tests available under `notebooks/`:
- **local_ingestion_test.ipynb**
- **rag_pipeline_demo.ipynb**

To run tests:
```
pip install -r requirements.txt
pytest
```

---

## 📜 API Usage  
Full API spec available in:  
📄 `docs/API_spec.md`

Example request:

```json
{
  "query": "What are the advantages of RAG architecture?"
}
```

---

## 🔗 Integrations
- Streamlit UI (optional)  
- Gradio chatbot interface (optional)  
- API Gateway REST endpoint  

---

🌍 Live Demo Links

🎯 Live App
🔗 https://udyam-sarthi-aide.lovable.app/

🎥 YouTube Video Demo
🔗 https://youtu.be/pVg2BOQyG-U

📝 Medium Blog Article
🔗 https://medium.com/@yessasvinis/the-50-000-chai-problem-how-im-building-india-s-first-compliance-gps-for-small-businesses-a47302a172f5


## 🧰 Requirements

```
python>=3.9
boto3
opensearch-py
langchain
pydantic
```

---

## 🤝 Contributing  
Pull requests are welcome. Please open an issue to discuss significant changes.

---

## 📄 License  
MIT License

---

## 🌟 Author  
Built by **Yessasvini Sudarshanam**  
Part of the **AI for Bharat – Context-Aware RAG Applications Workshop**

