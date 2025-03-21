# Data Formatting in the German ePA/eGK Infrastructure

The German electronic patient record (ePA) and electronic health card (eGK) infrastructure are central to achieving seamless and secure data exchange between healthcare providers. This document explains how medical data is formatted and structured to ensure interoperability, data integrity, and security in compliance with the standards set by gematik and related regulatory bodies.

## Data Formatting Standards

To achieve these objectives, the system uses several key standards:

- **HL7 FHIR**: Fast Healthcare Interoperability Resources (FHIR) is widely adopted to model health data. It supports data exchange via standardized APIs and provides resources for clinical, administrative, and financial data.
- **IHE Profiles**: Integrating the Healthcare Enterprise (IHE) profiles such as IHE XDS and IHE XCA ensure that documents and images are exchanged consistently across different systems.
- **Medical Information Objects (MIO)**: These objects define the structure and semantics for specific clinical data (e.g., laboratory results, imaging reports) to ensure that data is both machine-readable and clinically meaningful.
- **XML/JSON Schemas**: Data transmitted via the telematics infrastructure is often formatted using XML or JSON based on predefined schemas to ensure consistency and validation across all systems.

## Data Flow and Integration

The process of data formatting within the ePA/eGK ecosystem involves several key steps:

1. **Data Collection and Input**  
   - Medical data is entered at the point of care using certified practice management systems.
   - Data includes patient demographics, clinical findings, diagnostic results, treatment reports, and emergency data (NFDM) stored on the eGK.

2. **Data Transformation and Structuring**  
   - Input data is mapped to standardized HL7 FHIR resources and MIO specifications.
   - The system converts legacy formats into the structured XML/JSON formats as defined by gematik.
   - Validation against these schemas ensures data integrity and compliance.

3. **Secure Data Packaging**  
   - The formatted data is encrypted and prepared for transmission via the telematics infrastructure.
   - Metadata (e.g., timestamps, document identifiers) is appended to facilitate seamless integration and audit trails.

4. **Data Exchange and Integration**  
   - Structured data is exchanged between healthcare providers using standardized APIs.
   - Connectors and secure interfaces (provided by gematik-certified solutions) ensure interoperability between different EHR systems.
   - Access control and granular permissions management allow patients to determine who can view or modify their data.

## Security and Interoperability

Ensuring data formatting standards are met is critical not only for interoperability but also for data security. Key measures include:
- **Encryption and Authentication**: Data is encrypted during transmission, and access is controlled via the eGK (using PIN-based authentication).
- **Checksum and Hash Verification**: Deterministic methods are used to verify that data has not been altered during processing.
- **Interoperable APIs**: Open standards ensure that data formatting is uniform, reducing the risk of errors during system-to-system communication.

## Summary Table

| **Step**                  | **Process**                                      | **Key Standards/Components**          |
|---------------------------|--------------------------------------------------|---------------------------------------|
| Data Collection           | Input of patient data via certified systems      | Practice management systems, eGK       |
| Data Transformation       | Mapping legacy data to structured formats        | HL7 FHIR, MIO, XML/JSON schemas        |
| Data Packaging            | Encryption and metadata tagging                  | Secure connectors, checksum validation |
| Data Exchange             | Transmission via telematics infrastructure       | IHE profiles, standardized APIs        |
| Access Control            | Granting and managing permissions                | Granular permissions, patient self-determination |

