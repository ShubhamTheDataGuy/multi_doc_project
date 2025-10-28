# Multi-Document RAG API Service

A powerful Retrieval-Augmented Generation (RAG) API service built with FastAPI, LangChain, and FAISS for intelligent document querying and analysis.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Setup & Installation](#setup--installation)
- [Azure Deployment](#azure-deployment)
- [Usage Instructions](#usage-instructions)
- [API Documentation](#api-documentation)
- [Testing & Validation](#testing--validation)
- [Future Enhancements](#future-enhancements)
- [License](#license)

## 🎯 Overview

This project provides a scalable RAG pipeline that allows users to upload documents, process them through advanced NLP techniques, and query them using natural language. The system leverages vector embeddings and semantic search to deliver accurate, context-aware responses with source attribution.

## ✨ Features

- **Multi-format Document Support**: Process PDF, DOCX, TXT, and more
- **Semantic Search**: FAISS-powered vector similarity search
- **RAG Pipeline**: LangChain integration for intelligent answer synthesis
- **Source Attribution**: Track answers back to specific document pages
- **RESTful API**: FastAPI-based endpoints with automatic documentation
- **Cloud-Ready**: Containerized deployment for Azure Web Apps
- **Comprehensive Testing**: Unit and integration test coverage

## 📁 Project Structure

```
project-root/  
├── app/                # Core application logic  
│   ├── main.py         # FastAPI application entry point  
│   ├── routers/        # API endpoints (upload, query)  
│   ├── services/       # Business logic (document parsing, vector DB, LangChain)  
│   └── models/         # Data models and schemas  
├── tests/              # Unit and integration tests  
├── docker/             # Docker configuration files  
├── config/             # Environment settings and secrets  
├── requirements.txt    # Python dependencies  
└── README.md           # This document  
```

## 🚀 Setup & Installation

### 1. Clone the Repository

```bash
git clone https://github.com/ShubhamTheDataGuy/multi_doc_project.git  
cd multi_doc_project  
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt  
```

### 3. Configure Environment Variables

Copy `.env.example` to `.env` and update with your API keys and configuration:

```bash
cp .env.example .env
```

Required environment variables:
- API keys for LLM services
- Database connection strings
- Storage paths
- Azure credentials (for cloud deployment)

### 4. Run Locally

```bash
uvicorn app.main:app --reload  
```

The API will be available at `http://localhost:8000`

## ☁️ Azure Deployment

### 1. Build Docker Image

```bash
docker build -t rag-api-service .  
```

### 2. Push to Azure Container Registry

```bash
az acr login --name <your-acr-name>  
docker tag rag-api-service <your-acr-name>.azurecr.io/rag-api:latest  
docker push <your-acr-name>.azurecr.io/rag-api:latest  
```

### 3. Deploy to Azure Web App

1. Use the Azure Portal to deploy the container from ACR
2. Set environment variables (API keys, paths) in App Settings
3. Configure scaling and monitoring as needed

## 📖 Usage Instructions

### Upload a Document

**Endpoint:** `POST /api/v1/upload`

**Request:**
```http
Content-Type: multipart/form-data  

FormData:  
- file: <document file>  
```

**Example with cURL:**
```bash
curl -X POST "http://localhost:8000/api/v1/upload" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@document.pdf"
```

### Query Documents

**Endpoint:** `POST /api/v1/query`

**Request:**
```json
{  
  "query": "What are the key findings in the document?",  
  "top_k": 5  
}  
```

**Response:**
```json
{  
  "answer": "Synthesized answer from documents",  
  "sources": [  
    {  
      "document_name": "report.pdf",  
      "page_number": 4,  
      "similarity_score": 0.92  
    }  
  ]  
}  
```

## 📚 API Documentation

### Interactive Documentation

Once the application is running, access the interactive API documentation:

- **Swagger UI**: `http://localhost:8000/docs`
- **ReDoc**: `http://localhost:8000/redoc`

### Key Features

- **Auto-generated Documentation**: From route metadata and Pydantic models
- **Request/Response Examples**: Interactive testing interface
- **Parameter Explanations**: Detailed descriptions for all endpoints
- **Schema Definitions**: Clear data structure specifications
- **Error Handling**: Comprehensive error response documentation

### API Metadata

- **Title**: Multi-Document RAG API Service
- **Version**: Available in API docs
- **License**: MIT License
- **Contact**: Available via repository issue tracker

## 🧪 Testing & Validation

### Run Tests

```bash
pytest tests/ --cov=app  
```

### Test Coverage Areas

- ✅ Document parsing and format validation
- ✅ Embedding generation accuracy
- ✅ FAISS index operations
- ✅ LangChain RAG pipeline effectiveness
- ✅ API endpoint functionality
- ✅ Request/response validation
- ✅ Error handling and edge cases

### Run Specific Test Suites

```bash
# Unit tests only
pytest tests/unit/

# Integration tests only
pytest tests/integration/

# With verbose output
pytest tests/ -v
```

## 🚀 Future Enhancements

- [ ] Add support for additional formats (PPTX, XLSX)
- [ ] Implement fine-tuning for domain-specific RAG pipelines
- [ ] Add a web interface for user interaction
- [ ] Introduce authentication and rate limiting
- [ ] Enhance monitoring and logging for production environments
- [ ] Implement caching for frequently queried content
- [ ] Add support for multi-language documents
- [ ] Enable real-time document updates and reindexing

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support & Contact

For questions, bug reports, or feature requests:

- Open an issue on [GitHub Issues](https://github.com/ShubhamTheDataGuy/multi_doc_project/issues)
- Check existing documentation at `/docs` endpoint
- Review closed issues for common solutions

---

**Built with ❤️ using FastAPI, LangChain, and FAISS**

*For detailed technical documentation and architecture diagrams, visit the [Wiki](https://github.com/ShubhamTheDataGuy/multi_doc_project/wiki).*
