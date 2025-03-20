# OpenDoctor-Spec

> Open Doctor - Like _Cursor.sh IDE but for personal medical history_

> [!NOTE] This repository of specification documents is optimized for viewing in Obsidian [obsidian.md/download](https://obsidian.md/download) Clone repository and open as an Obsidian vault 
> 
## Overview & Project Story
Open Doctor is a specialized IDE designed for managing and interacting with medical history, similar to how Cursor IDE is used for coding. It provides a comprehensive platform for patients to maintain, understand, and share their medical records while ensuring privacy and data security. 
### The Problem
In today's healthcare system, both patients and doctors face significant challenges:
- Patients feel frustrated with limited time during doctor visits
- Doctors are increasingly overloaded with more patients and less time per person
- Critical medical history is often fragmented across different healthcare providers [↗ DataSources.md](DataSources.md)
- Important details from past visits and tests are frequently missed in brief consultations
- Patients struggle to maintain a comprehensive view of their health status
### Our Solution
Open Doctor is a privacy-first, open-source tool that empowers patients to take charge of their medical records. It provides:
- A comprehensive, always-current "one-pager" health summary for doctor visits
- Clear documentation of acute and chronic symptoms
- Complete historical test results and references
- Local AI-powered analysis of medical history
- Future integration with medical research databases for treatment protocol suggestions
### Key Differentiators
- **Privacy-First**: All processing happens locally on the patient's device
- **Open Source**: The only open-source AI doctor tool focused on local processing of patient health histories
- **Patient-Centric**: Empowers patients to maintain and understand their medical records
- **Doctor-Friendly**: Provides clear, concise summaries for efficient consultations
- **Future-Ready**: Will integrate with medical research for evidence-based treatment suggestions. [↗ See BenchmarkingDatasets.md for growing list of validation datasets](BenchmarkingDatasets.md)
----
## System Architecture
[↗ Full details in SystemArchitecture.md](SystemArchitecture.md)
### Core Components

**1. System Portability**

The system is engineered for full portability, enabling patients to securely store and manage their medical records directly on their own devices. This includes:
- A portable patient data file system.
- A flexible database schema optimized for diverse medical records.
- A self-contained LLM server stack that enables local AI processing without relying on external services.

**2. Asynchronous Background Processes**

The system employs asynchronous background processes to ensure data security and efficient operation without interrupting the core medical timeline. Key features include:
- **Process Tasks File:** All required background tasks are defined within a dedicated process tasks file. These tasks can run automatically in the background or be manually initiated by the user when needed.
- **Commissioning of Specific Tasks:** Certain process tasks—especially those requiring advanced AI computation or human oversight—can be commissioned separately. This ensures that critical updates and verifications occur without being directly committed to the patient's medical timeline.
- **Granular Permissions Management:** Detailed access control for sensitive medical data, ensuring that only authorized processes can modify records.
- **Secure File System Traversal:** Robust mechanisms for safely navigating and accessing the file system containing medical records.
- **Protected File Edit APIs:** APIs designed for secure and controlled updates to medical records.
- **Multi-Database Scheduler:** An efficient scheduler that orchestrates tasks across multiple databases, ensuring optimal data management and system performance.

**3. Frontend Interface**
[↗ More details in FrontendInterface.md](FrontendInterface.md)

The interface is designed to be intuitive and efficient, mirroring Cursor's coding tool layout but specialized for medical documents:

- **Right Side**: Collapsible file system view for easy navigation of medical records
- **Middle View**: 
  - Interactive timeline of medical history
  - Chronological organization of medical documents
  - Smooth scrolling with inertia animation
  - Quick access to the "State of health one pager" with PDF export
- **Left Side**: 
  - AI-powered chat interface for medical history queries
  - Smart forms for symptom and medication tracking
  - Local RAG pipeline for secure medical data analysis
  - Git-based version control for medical history

| ![](Linked%20files/Screenshot%202025-03-19%20at%2008.53.37.png) | ![](attachments/Pasted%20image%2020250320152756.png) |
| --------------------------------------------------------------- | ---------------------------------------------------- |

---
### Developer Tools
[↗ Complete documentation in DeveloperTools.md](DeveloperTools.md)

#### 1. Open Doctor LLM Agent Runtime MAKER
This tool ensures consistent and secure AI processing:
- Packages Open Doctor agent dependencies into a single binary
- Generates secure file hashes for verification
- Maintains deterministic processing for reliable results

#### 2. Medical Qualifications Permission Assigner
This component manages AI model capabilities and permissions:
- Provides AI "Open Dr ranking" for different medical specialties
- Registers model qualifications with the background scheduler
- Manages the tool database for medical interventions

## Open Doctor LLM Agent Runtimes
[↗ In-depth specifications in LLMAgentRuntimes.md](LLMAgentRuntimes.md)

### Requirements
The system requires specific components to ensure reliable and secure operation:
- Local or API access for data processing
- Deterministic seed numbers for consistent results
- Standardized prompts/chains/MCP-tools
- Compiled, hashed, and signed binaries for public distribution

### Deterministic Nature
> [!IMPORTANT]
> All doctors will be tested on deterministic outputs - temperature values are levels of statistically bound randomness. For this reason, all tests will be written with temperature value zero. Or use predefined temperature Seed values.  (difficult for when models are provided by external API calls.)

This ensures consistent and reliable medical advice:
- Temperature seed values are hardcoded
- Prompts and conversation chains are hardcoded
- Tools and APIs are hardcoded

> [!NOTE]
> Deterministic : Given the same input tokens, a doctor agent will need to always generate the same output tokens 100% of the time. 

###  Some early Testing Requirements: 
> [!TODO]
>- [ ] Validate LLM determinism in practice and identify
>- [ ] Test Tool APIs with Deterministic "dummy data" Implement on MCP_test servers
> 
> 
> [↗ See ProjectTODO.md for complete task list](ProjectTODO.md)

## Standards
[↗ Comprehensive standards documentation in StandardsAndAPI.md](StandardsAndAPI.md)

### Medical AI Standards
The system adheres to strict standards for medical AI interactions:

1. Patient Interactions:
   - Natural language query conversations
   - AI-assisted intake forms
   - Comprehensive history tracking
   - Clear health status summaries

2. Doctor Interactions:
   - Efficient knowledge queries
   - Detailed medical timelines
   - Concise health status reports

### Benchmark Standards
The system maintains high standards for medical accuracy and safety:
- Rigorous medical qualifications testing
- Comprehensive safety standards:
  - Granular patient data permissions
  - Controlled AI conversation levels
  - Hallucination detection
  - Immutable data tracking
  
[↗ See BenchmarkingDatasets.md for validation processes](BenchmarkingDatasets.md)

### API Standards
The system provides clear standards for integration and development:
- Secure database permission protocols
- Comprehensive runtime development guidelines
- Verified LLM agent runtime compilation
- Clear publication guidelines

> [!NOTE]
> Open Doctor is committed to maintaining the highest standards of medical accuracy, patient privacy, and system reliability while providing an open-source solution for better healthcare outcomes. [↗ See ExpertContacts.md for medical domain experts](ExpertContacts.md)

## Project Documentation

The following documents provide detailed information about different aspects of the Open Doctor project:

### Core Architecture and Components

- [SystemArchitecture.md](SystemArchitecture.md) - Detailed overview of the system architecture, core components, and security considerations.
- [FrontendInterface.md](FrontendInterface.md) - Comprehensive description of the user interface design, features, and interaction patterns.
- [DeveloperTools.md](DeveloperTools.md) - Documentation of tools available for developers to extend and customize the Open Doctor system.
- [LLMAgentRuntimes.md](LLMAgentRuntimes.md) - Specifications for LLM agent runtimes, including deterministic behavior and testing requirements.
- [StandardsAndAPI.md](StandardsAndAPI.md) - Standards and guidelines for medical AI, benchmarking, and API integration.

### Project Planning and Resources

- [ProjectRoadmap.md](ProjectRoadmap.md) - Future development plans, including core phases, key milestones, and planned enhancements.

- [Contributing.md](Contributing.md) - Guidelines for contributing to Open Doctor, including coding standards, pull request processes, and community resources.

- [ProjectTODO.md](ProjectTODO.md) - Comprehensive task list for project implementation, organized by priority and area of development.

### Data and Information Resources

- [MedicalDictionaries.md](MedicalDictionaries.md) - List of medical dictionaries and resources for terminology understanding and patient communication.

- [DataSources.md](DataSources.md) - Authoritative medical data sources for knowledge panels and dictionary data.

- [BenchmarkingDatasets.md](BenchmarkingDatasets.md) - Process and requirements for obtaining medical datasets for AI model validation.

### Community and Collaboration

- [ExpertContacts.md](ExpertContacts.md) - List of experts in medical informatics and healthcare technology for project guidance.
