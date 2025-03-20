# OpenDoctor-Spec

> Open Doctor - Like _Cursor.sh IDE but for medical history_

## Project Story

### The Problem
In today's healthcare system, both patients and doctors face significant challenges:
- Patients feel frustrated with limited time during doctor visits
- Doctors are increasingly overloaded with more patients and less time per person
- Critical medical history is often fragmented across different healthcare providers
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
- **Future-Ready**: Will integrate with medical research for evidence-based treatment suggestions

## Overview
Open Doctor is a specialized IDE designed for managing and interacting with medical history, similar to how Cursor IDE is used for coding. It provides a comprehensive platform for patients to maintain, understand, and share their medical records while ensuring privacy and data security.

## System Architecture

### Core Components

#### 1. System Portability
The system is designed to be fully portable, allowing patients to maintain their medical records securely on their own devices. This includes:
- A portable patient data file system
- A flexible database schema for medical records
- A self-contained LLM server stack for local AI processing

#### 2. Background Processes
The system includes robust background processes to ensure data security and efficient operation:
- Granular permissions management for sensitive medical data
- Secure file system traversal for medical records
- Protected file edit APIs for record updates
- Multi-database scheduler for efficient data management

#### 3. Frontend Interface
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

![Interface Screenshot](Linked%20files/Screenshot%202025-03-19%20at%2008.53.37.png)

### Developer Tools

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

### Testing Requirements: 
> [!TODO]
> - [ ] Test Tool APIs with Deterministic "dummy data" Implement on MCP_test servers
> - [ ] Validate LLM determinism in practice, identify and eliminate 

## Standards

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

### API Standards
The system provides clear standards for integration and development:
- Secure database permission protocols
- Comprehensive runtime development guidelines
- Verified LLM agent runtime compilation
- Clear publication guidelines

> [!NOTE]
> Open Doctor is committed to maintaining the highest standards of medical accuracy, patient privacy, and system reliability while providing an open-source solution for better healthcare outcomes.
