# ICD Database Vectorization for Open Doctor Project

## Project Summary

This project aims to develop a vector database system for the International Classification of Diseases (ICD) database maintained by the World Health Organization. The core functionality will allow for natural language queries of medical symptoms and conditions to retrieve the appropriate ICD codes and related medical interventions.

### Background

The ICD database is the internationally recognized standard for classifying diseases, symptoms, and medical conditions. Every country has their own version of this database, but the global standard is maintained in English by the WHO. The database contains codes for all known diseases and medical conditions, providing a standardized way to classify and communicate about medical diagnoses.

Currently, the ICD database is accessible through a REST API but lacks efficient natural language query capabilities and vector search functionality. This project aims to fill this gap by creating a vector representation of the ICD database to enable more intuitive searching based on patient-described symptoms.

### Project Goals

1. Create a vector database of the ICD-11 disease/symptom codes 
2. Build a similar vector database for medical interventions
3. Develop an API that allows natural language queries to find relevant ICD codes
4. Link diagnosis codes to appropriate intervention codes
5. Implement comprehensive testing for all components
6. Document the system for future developers and integration with the Open Doctor project

## Technical Architecture

The project will utilize the following technologies:

- **Vector Database**: Using an embedding model to convert medical terms and descriptions into vector representations
- **FastAPI**: For creating a REST API that serves vector search results
- **ICD-11 API**: The WHO's official API for accessing ICD codes and descriptions
- **Testing Framework**: Pytest for comprehensive testing of all components
- **GitHub Actions**: For continuous integration and test automation
- **Docker**: For containerization and easy deployment

## Student Roles and Responsibilities

The project is divided among six students, each with specific responsibilities:

1. **Project Manager & API Designer** - [Student 1](./Student1_ProjectManager.md)
   - Coordinates the team and ensures deliverables are met
   - Designs the API endpoints and response formats
   - Integrates the individual components
   - Estimated time: 40-45 hours

2. **ICD Database Specialist** - [Student 2](./Student2_ICDSpecialist.md)
   - Studies the ICD-11 database structure
   - Implements data extraction from ICD-11 API
   - Documents the ICD code hierarchy and relationships
   - Estimated time: 35-40 hours

3. **Vector Database Engineer** - [Student 3](./Student3_VectorDB.md)
   - Selects and implements the vector database solution
   - Creates embedding pipeline for medical terms
   - Optimizes vector search algorithms
   - Estimated time: 40-45 hours

4. **Medical Interventions Specialist** - [Student 4](./Student4_Interventions.md)
   - Researches medical intervention codes
   - Creates mappings between conditions and interventions
   - Builds the intervention vector database
   - Estimated time: 35-40 hours

5. **Testing Specialist** - [Student 5](./Student5_Testing.md)
   - Creates comprehensive test cases
   - Implements CI/CD pipeline
   - Ensures deterministic test results
   - Documents test coverage and results
   - Estimated time: 30-35 hours

6. **Documentation & Integration Specialist** - [Student 6](./Student6_Documentation.md)
   - Creates technical documentation
   - Prepares project report
   - Ensures system can be integrated with Open Doctor
   - Develops user guides and examples
   - Estimated time: 30-35 hours

## Timeline

- **Week 1** (April 19-25): Research and planning
  - Study ICD database structure
  - Select vector database technology
  - Design system architecture
  - Write initial tests

- **Week 2** (April 26-May 2): Core implementation
  - Extract ICD codes and descriptions
  - Implement vector database
  - Create basic API endpoints
  - Begin linking diagnoses and interventions

- **Week 3** (May 3-9): Integration and testing
  - Connect all components
  - Implement comprehensive testing
  - Optimize search performance
  - Begin documentation

- **Week 4** (May 10-16): Finalization
  - Complete documentation
  - Finalize code
  - Prepare presentation
  - Create final report

- **Final Submission**: May 25, 2025

## Success Criteria

The project will be considered successful if:

1. The system can accurately match natural language descriptions of symptoms to relevant ICD codes
2. Appropriate medical interventions are linked to diagnoses
3. The API responds to queries in under 1 second
4. Test coverage exceeds 85%
5. The system can be easily integrated with the Open Doctor project

## Communication and Collaboration

- **GitHub**: All code and documentation will be stored in a GitHub repository
- **Weekly Meetings**: Team will meet twice weekly to review progress
- **Slack/Discord**: Daily communication for quick updates and questions
- **Documentation**: Maintained in Markdown format within the repository

## Getting Started

Each team member should:

1. Review their specific role document linked above
2. Clone the repository and set up the development environment
3. Complete their assigned initial research tasks
4. Participate in the first team meeting to discuss architecture and approach

## Contact

If you have questions about the Open Doctor project or need technical guidance, please contact SG. 