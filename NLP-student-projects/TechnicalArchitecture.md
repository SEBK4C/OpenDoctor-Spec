# Technical Architecture: ICD Vectorization System

## Overview

This document outlines the technical architecture for the ICD Vectorization System, designed to enable natural language querying of medical conditions and their appropriate interventions. The system transforms the WHO's ICD-11 database into vector representations that can be efficiently searched using natural language queries.

## System Components

The system consists of the following major components:

### 1. Data Extraction and Processing

![Data Extraction Flow](https://mermaid.ink/img/pako:eNp1kM1qwzAQhF9F7Ln9QA4hYJpDTi2U0kN6EfJaViuikSXkVUpw3n3lOG5aoQezO_PNwO4FWm8QGhha1zcm4kcTG2NpYIWvh2IlGkcNdU9GJVZ-6H2gt6TXmW9Mdtn2uQm4KbNzm33rh80cjvjpWaEd-J1y9yJzIcdSYqgymyVzOJFrZYlPc_jrY7FEG41fXEPRV9Ym9BgFWjPqADG1ThUWahQHFZMJpTiHzrYUgLl27aYYrTvKwPDWUcSxTkRvefHnUdwFdPtxA3sFiZJByTCDw-S7m7NFMuVNBrcLuF_WX5LDEBWpL2MKBNXpWcYKiUF_B0WBBCqc4hXaYbqV4o6GCTJJtgaDf7rTfNrhsZIlzEotpClLVZXbXO3LotY7uT9U9QHKB4I7?type=png)

- **ICD API Client**: Connects to WHO's ICD-11 API to extract disease/condition codes and descriptions
- **Intervention Data Collector**: Gathers medical intervention codes and descriptions from relevant sources
- **Data Preprocessor**: Cleans and normalizes medical terminology, prepares data for vectorization
- **Entity Relationship Manager**: Establishes connections between conditions and appropriate interventions

### 2. Vector Database System

![Vector Database System](https://mermaid.ink/img/pako:eNp1kstqwzAQRX9FzDr5gCxCwbQLbwotdNFuRDxWNYponEj1gyTE_15ZTpq2YDY3c-88GHUEKKRGTKDrbe1VwJ3STvnYKp-P2WKW1R05ah4YJSv5e9-Lw1VYp2ylelsdpuFTk2_7_KvXzWE-HTw8C5y9uI34MBNJkqYJOczn8-kkYk_Gnsr3p9NP37JYa-SXVJfsjVSe2sA9S2t6ZVFg45TFLnCHteaeXOZD6XPlETWJStRdqTn0PMIY5aiiNhQwnNYp9NQAXVUICFz62rDBKMXhXMLijTLIAxsVrPjyJEHcrXI2qXKbqJC-wlvkQHy1fIPkBgp4AqcVOLIuTpI_XB1O_R6ShCyQbFH_b17FiRbKxdehMQNKmw7j1SMacXiHlAEjKKNlE-nCdYXpBtGCDqD3oNBgu54uy5yOmRZUZUbFmZGE851O9ls99bpLvgHUfH0u?type=png)

- **Vector Embedding Engine**: Converts medical text into vector representations
- **Vector Storage System**: Efficiently stores and indexes vector embeddings
- **Similarity Search Module**: Performs efficient nearest-neighbor search in vector space
- **Ranking and Relevance Engine**: Scores and ranks search results based on relevance

### 3. API Layer

![API Layer](https://mermaid.ink/img/pako:eNp1kc1Ow0AMhF_F8jkPkANSBYIDJ1qpUg_0Erle2kU4m9bbICHEu-NNW6DiqDNj-_PYewStswQF9I2tKu3p1ehaW9LUiy_bapZUlmrqHh0pJf703fvdUVZn2avr2s0w_dTUm77-6ly9m42Db7dI3r_dmXxI8jzPDnxGg2wPxZvj8f179h6VIXcU6pztjbQ0cEDX6F55YrLa0cDeE7yeBvRVQJtNVQWySJ5EI6sh1WStxgC6jXt0GFG9REc-SlhYOsNRJLQnCIcnmrzhRZijY0zZ7VW5jdOYsWYXxB_hm-RAfLXyDYpbKMQTOK1ICdflZfCXyyZT_wRFEgu02WT_F-ZKLF4pB5-GpjOgMm1iKz0hq70fUGRgBW1s2Zi7cV2J7hAdeA1mD5Ysbe_Hw3K1x8xrqQtDWWFAPp_N-ePkNBhw8AMWGaoU?type=png)

- **FastAPI Server**: Provides RESTful API endpoints for querying the vector database
- **Request Processor**: Handles incoming requests, validates parameters
- **Response Formatter**: Structures API responses consistently
- **Authentication & Rate Limiting**: Optional components for production deployments

### 4. Testing and Quality Assurance

![Testing Framework](https://mermaid.ink/img/pako:eNptUctOwzAQ_BVrz_kADkiVgAMnKFKlHuBSxd40W-JsYm-DiPLv2GkKRRzX45mdxz4EaoNDSaB3rm6sp3enG-upY4-_x2JOhaeW-ncvSpXCdPSxeh7ENvKFb5vVMP3W5Mu-_Bi9X82mw8PDtWbnx0-VHhNjTHbkd2wwimIFrjdmPrFHcq0s2dMc_vpcXKKzzt-5uqSvQgbqPUYxreuVQ8Gtk0fmXuzQeSrpqnKxFnOAo9IW9V0wGHoeZI7NUUXtOWCcPSj01DJdVUwoXPrGssOghO-DwPyt8igh8NAj83lD5jDC1RJX1EBe1KGH9GlxF9TDyS_IX1CBz-C1Yoe8STk5-Tk7nsxzlCdJYdju8v-P78TRK-Xj_2h5ApRu56PWnjy7w4jJhBLouLLD0FVcndAtssOk0a9B4dBt-2Gc-zgpE5cXljNTWInjOOfXs8voO8efP_eCi64?type=png)

- **Unit Testing Framework**: Tests individual components in isolation
- **Integration Testing System**: Tests interactions between components
- **End-to-End Testing**: Validates complete system behavior
- **CI/CD Pipeline**: Automates testing and deployment processes

## Data Flow

The typical data flow through the system is as follows:

1. **Data Collection Phase**
   - ICD-11 codes and descriptions are extracted from the WHO API
   - Intervention codes and descriptions are collected from medical sources
   - Data is cleaned, normalized, and preprocessed

2. **Vectorization Phase**
   - Medical terms and descriptions are converted to vector embeddings
   - Vectors are indexed and stored in the vector database
   - Links between diagnoses and interventions are established

3. **Query Processing Phase**
   - User sends natural language query about symptoms or conditions
   - Query is converted to vector representation
   - Similarity search identifies relevant ICD codes
   - Related interventions are retrieved
   - Results are ranked and formatted
   - Response is returned to the user

## Technology Stack

The system will be built using the following technologies:

- **Programming Language**: Python 3.9+
- **API Framework**: FastAPI
- **Vector Database**: FAISS, Pinecone, or similar
- **Embedding Models**: Sentence-BERT, MedicalBERT, or similar
- **Testing**: Pytest
- **CI/CD**: GitHub Actions
- **Documentation**: Markdown, Sphinx
- **Containerization**: Docker

## Database Schema

### ICD Code Dataset

```
{
  "code": "AB12.3",           # ICD-11 code
  "title": "Disease Name",    # Official disease/condition name
  "description": "...",       # Detailed description
  "inclusions": ["...", "..."], # Related conditions included
  "exclusions": ["...", "..."], # Related conditions excluded
  "parents": ["AA00", "AA10"], # Parent codes in hierarchy
  "children": ["AB12.31", "AB12.32"], # Child codes
  "synonyms": ["...", "..."], # Alternative names
  "vector": [0.1, 0.2, ...],  # Vector representation
}
```

### Intervention Dataset

```
{
  "code": "XYZ-123",           # Intervention code
  "title": "Procedure Name",   # Intervention name
  "description": "...",        # Detailed description
  "category": "Medication",    # Type of intervention
  "related_conditions": ["AB12.3", "CD45.6"], # Related ICD codes
  "contraindications": ["EF78.9"], # ICD codes where this is contraindicated
  "vector": [0.3, 0.4, ...],   # Vector representation
}
```

## API Endpoints

### Core Endpoints

- `POST /api/v1/search/conditions`
  - Searches for conditions/diseases based on symptoms
  - Accepts natural language descriptions
  - Returns relevant ICD codes with confidence scores

- `GET /api/v1/condition/{icd_code}`
  - Returns detailed information about a specific ICD code
  - Includes description, inclusions, exclusions, etc.

- `GET /api/v1/condition/{icd_code}/interventions`
  - Returns interventions associated with a specific ICD code
  - Ranked by relevance

- `POST /api/v1/search/interventions`
  - Searches for interventions based on natural language queries
  - Returns relevant intervention codes with descriptions

### Utility Endpoints

- `GET /api/v1/health`
  - System health check endpoint

- `GET /api/v1/metrics`
  - Returns system metrics and statistics

## Deployment Architecture

For the NLP project, the system will be deployed as:

1. **Local Development**: Docker containers for each component
2. **Testing Environment**: Containerized deployment for testing
3. **Final Demonstration**: Fully integrated system with sample frontend

For future integration with Open Doctor, the system can be:

1. **Self-hosted**: Deployed as Docker containers or Kubernetes pods
2. **Cloud-based**: Deployed on AWS, GCP, or Azure
3. **Edge-friendly**: Components can be optimized for edge deployment

## Performance Considerations

- Vector database should be optimized for fast similarity search
- API response times should be under 1 second
- System should handle concurrent requests efficiently
- Caching mechanisms may be implemented for common queries

## Security Considerations

- All medical data should be handled according to healthcare privacy standards
- API authentication and authorization for production deployments
- Input validation to prevent injection attacks
- Rate limiting to prevent abuse

## Future Extensions

- Support for multiple languages beyond English
- Integration with electronic health record systems
- Personalized intervention recommendations based on patient history
- Mobile-optimized API for smartphone applications
- Real-time updating of medical knowledge as ICD codes evolve

## References

- [WHO ICD-11 API Documentation](https://icd.who.int/icdapi)
- [Vector Database Best Practices](https://www.pinecone.io/learn/vector-database/)
- [FastAPI Documentation](https://fastapi.tiangolo.com/) 