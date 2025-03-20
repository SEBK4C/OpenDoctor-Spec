# Sample Code for ICD Vectorization Project

This document provides code examples to help students get started with various aspects of the project. These examples are meant to serve as starting points and should be adapted to meet the specific requirements of your component.

## ICD API Client

This example shows how to make requests to the ICD-11 API and handle the responses.

```python
import requests
import json
import os
from typing import Dict, List, Any
import time

class ICD11ApiClient:
    """
    A client for interacting with the ICD-11 API
    """
    def __init__(self, client_id: str, client_secret: str):
        self.client_id = client_id
        self.client_secret = client_secret
        self.base_url = "https://id.who.int/icd/entity"
        self.token = None
        self.token_expiry = 0
        
    def _get_token(self) -> str:
        """
        Get an OAuth token for the ICD API
        """
        if self.token and time.time() < self.token_expiry:
            return self.token
            
        url = "https://icdaccessmanagement.who.int/connect/token"
        payload = {
            "client_id": self.client_id,
            "client_secret": self.client_secret,
            "scope": "icdapi_access",
            "grant_type": "client_credentials"
        }
        headers = {
            "Content-Type": "application/x-www-form-urlencoded"
        }
        
        response = requests.post(url, data=payload, headers=headers)
        response.raise_for_status()
        
        token_data = response.json()
        self.token = token_data["access_token"]
        self.token_expiry = time.time() + token_data["expires_in"] - 60  # Buffer of 60 seconds
        
        return self.token
    
    def get_entity(self, entity_id: str) -> Dict[str, Any]:
        """
        Get details for a specific ICD entity
        """
        token = self._get_token()
        url = f"{self.base_url}/{entity_id}"
        
        headers = {
            "Authorization": f"Bearer {token}",
            "Accept": "application/json",
            "API-Version": "v2",
            "Accept-Language": "en"
        }
        
        response = requests.get(url, headers=headers)
        response.raise_for_status()
        
        return response.json()
    
    def search_entities(self, query: str, limit: int = 10) -> List[Dict[str, Any]]:
        """
        Search for ICD entities based on a query string
        """
        token = self._get_token()
        url = "https://id.who.int/icd/release/11/2023-01/mms/search"
        
        params = {
            "q": query,
            "limit": limit
        }
        
        headers = {
            "Authorization": f"Bearer {token}",
            "Accept": "application/json",
            "API-Version": "v2",
            "Accept-Language": "en"
        }
        
        response = requests.get(url, params=params, headers=headers)
        response.raise_for_status()
        
        return response.json().get("destinationEntities", [])

# Example usage
if __name__ == "__main__":
    client_id = os.getenv("ICD_CLIENT_ID")
    client_secret = os.getenv("ICD_CLIENT_SECRET")
    
    if not client_id or not client_secret:
        print("Please set ICD_CLIENT_ID and ICD_CLIENT_SECRET environment variables")
        exit(1)
    
    client = ICD11ApiClient(client_id, client_secret)
    
    # Search for diabetes
    results = client.search_entities("diabetes")
    print(f"Found {len(results)} results for 'diabetes'")
    
    for result in results[:3]:  # Show first 3 results
        print(f"Title: {result['title']}")
        print(f"ID: {result['id']}")
        print(f"Definition: {result.get('definition', 'No definition available')}")
        print("---")
    
    # Get details for a specific entity
    entity = client.get_entity("http://id.who.int/icd/entity/1580976949")
    print(f"Entity details for {entity['title']}:")
    print(json.dumps(entity, indent=2))
```

## Vector Embedding

This example demonstrates how to create vector embeddings of medical text using sentence transformers.

```python
import numpy as np
from typing import List, Dict, Any, Union
from sentence_transformers import SentenceTransformer
import pandas as pd
import json

class MedicalTextEmbedder:
    """
    Creates vector embeddings for medical text using sentence transformers
    """
    def __init__(self, model_name: str = "all-MiniLM-L6-v2"):
        """
        Initialize with a specific model
        Consider using medical-specific models like:
        - 'pritamdeka/BioBERT-mnli-snli-scinli-scitail-mednli-stsb'
        - 'microsoft/BiomedNLP-PubMedBERT-base-uncased-abstract-fulltext'
        """
        self.model = SentenceTransformer(model_name)
        self.vector_dim = self.model.get_sentence_embedding_dimension()
        print(f"Loaded model with dimension: {self.vector_dim}")
        
    def embed_text(self, text: str) -> np.ndarray:
        """
        Create a vector embedding for a single text string
        """
        return self.model.encode(text)
    
    def embed_batch(self, texts: List[str]) -> np.ndarray:
        """
        Create vector embeddings for a batch of texts
        """
        return self.model.encode(texts)
    
    def process_icd_entity(self, entity: Dict[str, Any]) -> Dict[str, Any]:
        """
        Process an ICD entity and add vector embeddings
        """
        # Combine relevant text for embedding
        text_to_embed = f"{entity['title']} {entity.get('definition', '')} {' '.join(entity.get('synonym', []))}"
        
        # Create embedding
        vector = self.embed_text(text_to_embed)
        
        # Add embedding to entity
        entity['vector'] = vector.tolist()
        
        return entity
    
    def process_icd_dataset(self, entities: List[Dict[str, Any]]) -> List[Dict[str, Any]]:
        """
        Process a list of ICD entities and add vector embeddings
        """
        processed_entities = []
        
        # Extract text for batch processing
        texts = []
        for entity in entities:
            text = f"{entity['title']} {entity.get('definition', '')} {' '.join(entity.get('synonym', []))}"
            texts.append(text)
        
        # Batch embed
        vectors = self.embed_batch(texts)
        
        # Add vectors back to entities
        for i, entity in enumerate(entities):
            entity_copy = entity.copy()
            entity_copy['vector'] = vectors[i].tolist()
            processed_entities.append(entity_copy)
        
        return processed_entities
    
    def save_embeddings(self, entities: List[Dict[str, Any]], output_file: str):
        """
        Save entities with embeddings to a file
        """
        with open(output_file, 'w') as f:
            json.dump(entities, f)
        
        print(f"Saved {len(entities)} embedded entities to {output_file}")

# Example usage
if __name__ == "__main__":
    # Sample ICD entities (normally these would come from the ICD API)
    sample_entities = [
        {
            "id": "http://id.who.int/icd/entity/1580976949",
            "title": "Diabetes mellitus",
            "definition": "A chronic condition characterized by hyperglycemia",
            "synonym": ["Diabetes", "DM"]
        },
        {
            "id": "http://id.who.int/icd/entity/1056888138",
            "title": "Hypertension",
            "definition": "Persistently high arterial blood pressure",
            "synonym": ["High blood pressure", "HTN"]
        }
    ]
    
    embedder = MedicalTextEmbedder()
    processed_entities = embedder.process_icd_dataset(sample_entities)
    
    # Show the first entity with its vector
    entity = processed_entities[0]
    print(f"Entity: {entity['title']}")
    print(f"Vector (first 5 elements): {entity['vector'][:5]}")
    print(f"Vector length: {len(entity['vector'])}")
    
    # Save to file
    embedder.save_embeddings(processed_entities, "icd_embeddings.json")
```

## FastAPI Server

This example shows how to set up a FastAPI server with endpoints for vector search.

```python
from fastapi import FastAPI, HTTPException, Query
from pydantic import BaseModel
from typing import List, Dict, Any, Optional
import numpy as np
import faiss
import json
import os
from sentence_transformers import SentenceTransformer

# Models for request/response
class SearchQuery(BaseModel):
    text: str
    max_results: int = 5
    min_score: float = 0.5

class ConditionResult(BaseModel):
    code: str
    title: str
    description: Optional[str] = None
    score: float

class SearchResponse(BaseModel):
    results: List[ConditionResult]
    query: str
    count: int

# Vector search engine
class VectorSearchEngine:
    def __init__(self, embedding_model: str = "all-MiniLM-L6-v2"):
        # Load model for embedding queries
        self.model = SentenceTransformer(embedding_model)
        self.vector_dim = self.model.get_sentence_embedding_dimension()
        
        # Initialize empty index
        self.index = faiss.IndexFlatIP(self.vector_dim)  # Inner product for cosine similarity
        self.entities = []
        
        print(f"Initialized vector search engine with dimension: {self.vector_dim}")
    
    def load_from_file(self, file_path: str):
        """
        Load embeddings from a JSON file
        """
        if not os.path.exists(file_path):
            raise FileNotFoundError(f"Embedding file not found: {file_path}")
        
        with open(file_path, 'r') as f:
            self.entities = json.load(f)
        
        # Extract vectors for FAISS index
        vectors = np.array([entity['vector'] for entity in self.entities], dtype=np.float32)
        
        # Normalize vectors for cosine similarity
        faiss.normalize_L2(vectors)
        
        # Build index
        self.index = faiss.IndexFlatIP(self.vector_dim)
        self.index.add(vectors)
        
        print(f"Loaded {len(self.entities)} entities into search index")
    
    def search(self, query: str, max_results: int = 5, min_score: float = 0.5) -> List[Dict[str, Any]]:
        """
        Search for entities similar to the query
        """
        # Create query embedding
        query_vector = self.model.encode([query])[0]
        query_vector = query_vector.reshape(1, -1).astype(np.float32)
        faiss.normalize_L2(query_vector)
        
        # Search index
        scores, indices = self.index.search(query_vector, k=max_results)
        
        # Format results
        results = []
        for i, idx in enumerate(indices[0]):
            if idx != -1 and scores[0][i] >= min_score:  # Valid index and meets minimum score
                entity = self.entities[idx]
                result = {
                    "code": entity.get("code", ""),
                    "title": entity.get("title", ""),
                    "description": entity.get("definition", ""),
                    "score": float(scores[0][i])
                }
                results.append(result)
        
        return results

# Initialize FastAPI
app = FastAPI(
    title="ICD Vector Search API",
    description="API for searching ICD codes using vector embeddings",
    version="0.1.0"
)

# Initialize search engine
search_engine = VectorSearchEngine()

@app.on_event("startup")
async def startup_event():
    """
    Load embeddings on startup
    """
    try:
        search_engine.load_from_file("icd_embeddings.json")
    except Exception as e:
        print(f"Warning: Could not load embeddings: {e}")
        print("API will not return search results until embeddings are loaded")

@app.post("/api/v1/search/conditions", response_model=SearchResponse)
async def search_conditions(query: SearchQuery):
    """
    Search for ICD conditions based on natural language description
    """
    results = search_engine.search(
        query=query.text,
        max_results=query.max_results,
        min_score=query.min_score
    )
    
    if not results:
        return SearchResponse(results=[], query=query.text, count=0)
    
    return SearchResponse(
        results=[ConditionResult(**result) for result in results],
        query=query.text,
        count=len(results)
    )

@app.get("/api/v1/health")
async def health_check():
    """
    Health check endpoint
    """
    return {"status": "ok", "entities_loaded": len(search_engine.entities)}

# Example usage
if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
```

## Testing with Pytest

This example demonstrates how to write tests for the vector search functionality.

```python
import pytest
import numpy as np
import json
import tempfile
import os
from unittest.mock import patch, MagicMock

# Import your modules (adjust as needed)
# from vector_search import VectorSearchEngine
# from icd_client import ICD11ApiClient

# For demonstration, we'll define a simplified version of the search engine
class SimpleVectorSearchEngine:
    def __init__(self):
        self.entities = []
        self.vectors = []
    
    def load_from_file(self, file_path):
        with open(file_path, 'r') as f:
            self.entities = json.load(f)
        self.vectors = [np.array(entity['vector']) for entity in self.entities]
    
    def search(self, query, max_results=5, min_score=0.5):
        # Simplified search that returns exact matches
        results = []
        for entity in self.entities:
            if query.lower() in entity['title'].lower():
                results.append({
                    "code": entity.get("code", ""),
                    "title": entity['title'],
                    "description": entity.get("definition", ""),
                    "score": 0.95
                })
                if len(results) >= max_results:
                    break
        return results

# Fixtures
@pytest.fixture
def sample_entities():
    return [
        {
            "code": "A01",
            "title": "Diabetes mellitus",
            "definition": "A chronic condition characterized by hyperglycemia",
            "vector": [0.1, 0.2, 0.3, 0.4, 0.5]
        },
        {
            "code": "A02",
            "title": "Hypertension",
            "definition": "Persistently high arterial blood pressure",
            "vector": [0.2, 0.3, 0.4, 0.5, 0.6]
        },
        {
            "code": "A03",
            "title": "Asthma",
            "definition": "A chronic respiratory condition",
            "vector": [0.3, 0.4, 0.5, 0.6, 0.7]
        }
    ]

@pytest.fixture
def embedded_entities_file(sample_entities):
    # Create a temporary file with embedded entities
    with tempfile.NamedTemporaryFile(mode='w', delete=False, suffix='.json') as f:
        json.dump(sample_entities, f)
        temp_file = f.name
    
    yield temp_file
    
    # Cleanup after test
    if os.path.exists(temp_file):
        os.remove(temp_file)

@pytest.fixture
def search_engine():
    return SimpleVectorSearchEngine()

# Tests
def test_vector_search_engine_init(search_engine):
    assert search_engine is not None
    assert hasattr(search_engine, 'search')
    assert hasattr(search_engine, 'load_from_file')

def test_load_embeddings(search_engine, embedded_entities_file, sample_entities):
    search_engine.load_from_file(embedded_entities_file)
    assert len(search_engine.entities) == len(sample_entities)

def test_search_finds_matching_entities(search_engine, embedded_entities_file):
    search_engine.load_from_file(embedded_entities_file)
    
    # Search for diabetes
    results = search_engine.search("diabetes")
    assert len(results) > 0
    assert any(r['title'] == 'Diabetes mellitus' for r in results)
    
    # Search for hypertension
    results = search_engine.search("hypertension")
    assert len(results) > 0
    assert any(r['title'] == 'Hypertension' for r in results)

def test_search_respects_max_results(search_engine, embedded_entities_file):
    search_engine.load_from_file(embedded_entities_file)
    
    # Add more entities that would match "a" query
    search_engine.entities.extend([
        {"title": "Anemia", "vector": [0.1, 0.1, 0.1, 0.1, 0.1]},
        {"title": "Arthritis", "vector": [0.2, 0.2, 0.2, 0.2, 0.2]},
        {"title": "Anxiety", "vector": [0.3, 0.3, 0.3, 0.3, 0.3]}
    ])
    
    # Search with max_results=2
    results = search_engine.search("a", max_results=2)
    assert len(results) <= 2

def test_search_with_no_matches(search_engine, embedded_entities_file):
    search_engine.load_from_file(embedded_entities_file)
    
    # Search for a term unlikely to match
    results = search_engine.search("xyzabc123")
    assert len(results) == 0

# Mock-based tests for external dependencies
def test_api_client_get_entity():
    # Example of mocking external API
    with patch('requests.post') as mock_post, patch('requests.get') as mock_get:
        # Mock token response
        mock_post.return_value.json.return_value = {
            "access_token": "fake_token",
            "expires_in": 3600
        }
        mock_post.return_value.raise_for_status = MagicMock()
        
        # Mock entity response
        mock_get.return_value.json.return_value = {
            "id": "http://id.who.int/icd/entity/1234567890",
            "title": "Test Disease",
            "definition": "A test disease for unit testing"
        }
        mock_get.return_value.raise_for_status = MagicMock()
        
        # Create client and test
        # client = ICD11ApiClient("test_id", "test_secret")
        # entity = client.get_entity("1234567890")
        
        # Assert expected result
        # assert entity["title"] == "Test Disease"
        
        # Since we're not importing the actual client, just verify mocks were called
        assert True  # Replace with actual test when implementing
```

## CI/CD Pipeline (GitHub Actions)

This example shows how to set up a GitHub Actions workflow for CI/CD.

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
        pip install pytest pytest-cov flake8
    
    - name: Lint with flake8
      run: |
        # stop the build if there are Python syntax errors or undefined names
        flake8 . --count --select=E9,F63,F7,F82 --show-source --statistics
        # exit-zero treats all errors as warnings
        flake8 . --count --exit-zero --max-complexity=10 --max-line-length=127 --statistics
    
    - name: Test with pytest
      run: |
        pytest --cov=./ --cov-report=xml
    
    - name: Upload coverage to Codecov
      uses: codecov/codecov-action@v1
      with:
        file: ./coverage.xml
        fail_ci_if_error: false

  build:
    runs-on: ubuntu-latest
    needs: test
    if: github.event_name == 'push' && github.ref == 'refs/heads/main'
    
    steps:
    - uses: actions/checkout@v2
    
    - name: Set up Python
      uses: actions/setup-python@v2
      with:
        python-version: '3.9'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install build twine
    
    - name: Build package
      run: |
        python -m build
    
    - name: Archive build artifacts
      uses: actions/upload-artifact@v2
      with:
        name: dist
        path: dist/
```

## Docker Configuration

This example provides Docker configuration files for containerizing the application.

```dockerfile
# Dockerfile
FROM python:3.9-slim

WORKDIR /app

# Install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy application code
COPY . .

# Run the application
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  api:
    build: .
    ports:
      - "8000:8000"
    volumes:
      - ./:/app
    environment:
      - ICD_CLIENT_ID=${ICD_CLIENT_ID}
      - ICD_CLIENT_SECRET=${ICD_CLIENT_SECRET}
    restart: unless-stopped
```

## Sample Project Structure

This is a recommended project structure for organizing your code:

```
icd-vector-search/
├── .github/
│   └── workflows/
│       └── ci.yml
├── api/
│   ├── __init__.py
│   ├── main.py          # FastAPI application
│   ├── models.py        # Pydantic models
│   └── routes/
│       ├── __init__.py
│       ├── conditions.py
│       └── interventions.py
├── data/
│   ├── __init__.py
│   ├── icd_client.py    # ICD API client
│   └── intervention_collector.py
├── tests/
│   ├── __init__.py
│   ├── test_api.py
│   ├── test_data.py
│   └── test_vector.py
├── vector/
│   ├── __init__.py
│   ├── embedder.py      # Vector embedding
│   └── search.py        # Vector search
├── .gitignore
├── Dockerfile
├── README.md
├── docker-compose.yml
└── requirements.txt
```

## Requirements.txt Example

```
# API
fastapi>=0.95.0
uvicorn>=0.21.1
pydantic>=1.10.7

# Data processing
requests>=2.28.2
pandas>=2.0.0
numpy>=1.24.2

# Vector search
sentence-transformers>=2.2.2
faiss-cpu>=1.7.4  # Use faiss-gpu for GPU acceleration

# Testing
pytest>=7.3.1
pytest-cov>=4.1.0
httpx>=0.24.0  # For FastAPI testing
```

Feel free to adapt these examples to your specific component and requirements. The provided code is meant to serve as a starting point and will need to be modified to fit into the complete system architecture. 