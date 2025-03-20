# OpenDoctor-Spec

> Open Doctor - Like _Cursor.sh IDE but for medical history_

## Overview
Open Doctor is a specialized IDE designed for managing and interacting with medical history, similar to how Cursor IDE is used for coding.

## System Architecture

### Core Components

#### 1. System Portability
- Fully portable system
- Patient data file system
- Database schema
- LLM server stack (packaged as single binary)

#### 2. Background Processes
- Permissions management
- File system traversal
- File edit APIs
- Multi-database scheduler

#### 3. Frontend Interface
The interface mirrors Cursor's coding tool layout but is specialized for medical documents:

- **Right Side**: Collapsible file system view
- **Middle View**: 
  - Date scroll with text summary of medical timeline
  - Oldest medical documents at bottom
  - Newest documents at top
  - Scroll with inertia animation
  - Snap page to "State of health one pager" with prominent "Export as PDF" button
- **Left Side**: 
  - Vertical split window for chat conversations
  - Horizontal split bottom for "Autonomous diagnosis - Smart Forms View"
  - Primary AI interaction point
  - RAG pipeline for patient data queries
  - Smart form generation for symptom/medication tracking
  - Git-based version control for medical history

![Interface Screenshot](Linked%20files/Screenshot%202025-03-19%20at%2008.53.37.png)

### Developer Tools

#### 1. Open Doctor LLM Agent Runtime MAKER
- Packages Open Doctor agent dependencies into single binary
- Generates file hashes

#### 2. Medical Qualifications Permission Assigner
- Provides AI "Open Dr ranking"
- Registers model qualifications with background scheduler
- Manages tool database

## Open Doctor LLM Agent Runtimes

### Requirements
- Local or API access
- Seed numbers
- Prompts/chains/MCP-tools
- Compiled, hashed, and signed for public distribution

### Deterministic Nature
> [!IMPORTANT]
> All doctors are deterministic - No randomness!

- Temperature seed values are hardcoded
- Prompts and conversation chains are hardcoded
- Tools and APIs are hardcoded

> [!NOTE]
> Given the same input tokens, an old doctor agent will always generate the same output tokens.

### Testing Requirements
> [!TODO]
> - [ ] Test Tool APIs with "dummy data"
> - [ ] Implement MCP_test server with dummy data list
> - [ ] Validate LLM determinism in practice

## Standards

### Medical AI Standards
1. Patient Interactions:
   - User query conversations
   - AI intake form and patient query
   - History tracking and medical timeline
   - State of patient "one pager"

2. Doctor Interactions:
   - Knowledge query conversations
   - Medical timelines
   - State of patient "one pager"

### Benchmark Standards
- Medical qualifications tests
- Safety standards:
  - Patient data permissions (API-tool_use-level 1,2,3,4...)
  - Patient conversation permissions (AI_level 1,2,3,4...)
  - Hallucination detection
  - Data change tracking and immutability (Git)

### API Standards
- Database permission request protocols
- Open Dr. runtime development guidelines
- "Known Good LLM agent runtimes" compilation and signing
- Runtime publication guidelines
