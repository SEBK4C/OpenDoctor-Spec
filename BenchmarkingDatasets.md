# Benchmarking Datasets

## Overview
This document outlines the process for acquiring and using comprehensive medical datasets for validating and benchmarking the Open Doctor system, with a particular focus on the Medical Information Mart for Intensive Care (MIMIC) database.

## Purpose
Medical benchmarking datasets are essential for:
- Validating AI model accuracy in medical contexts
- Testing system responses against known medical cases
- Ensuring compliance with medical standards
- Measuring performance improvements over time
- Identifying areas for enhancement in medical knowledge

## Resources

### MIMIC Database
**Publisher**: PhysioNet (MIT Laboratory for Computational Physiology)  
**Website**: [MIMIC](https://mimic.mit.edu/)  
**Description**: MIMIC is a large, freely-available database comprising de-identified health data associated with ~60,000 intensive care unit admissions. It includes demographics, vital signs, laboratory tests, medications, and more.

### Other Recommended Datasets
- **i2b2** (Informatics for Integrating Biology & the Bedside)
- **N2C2** (National NLP Clinical Challenges)
- **MedPix** (Medical image database from NLM)
- **Cancer Imaging Archive** (TCIA)

## Requirements Note

> [!IMPORTANT]
> Access to MIMIC requires completion of a training course in human research subject protection and HIPAA guidelines. All team members who will access the data must complete this training.

## Benchmarking Process

### Dataset Access Protocol

#### Step 1: Complete Required Training
1. Visit the [CITI Program website](https://about.citiprogram.org/programs/human-subjects-research-hsr/)
2. Register and complete the "Data or Specimens Only Research" course
3. Save your completion certificate as a PDF

#### Step 2: Request PhysioNet Account
1. Create an account on [PhysioNet](https://physionet.org/register/)
2. Complete your profile with professional information
3. Specify institutional affiliation (or independent researcher status)

#### Step 3: Apply for MIMIC Access
1. Navigate to the [MIMIC-III project page](https://physionet.org/content/mimiciii/1.4/)
2. Click "Request Access"
3. Upload your CITI completion certificate
4. Agree to the data use agreement
5. Provide project description focused on benchmarking medical AI systems

#### Step 4: Credentialing Process
1. Wait for approval (typically 3-5 business days)
2. Respond promptly to any additional information requests
3. Once approved, download the data or access via cloud platforms

### Application Process
The application for MIMIC access should include:

1. **Project Title**: "Open Doctor Medical AI Benchmarking and Validation"

2. **Research Summary**:
   - Purpose: Validation and benchmarking of medical AI systems
   - Methodology: Comparison of system outputs against known medical cases
   - Expected outcomes: Quantitative metrics on accuracy and safety
   - Benefit: Development of safer, more accurate medical information systems

3. **Data Usage Plan**:
   - Storage: Secured environment with appropriate controls
   - Access: Limited to essential team members with completed training
   - Analysis: Non-identifying statistical analysis only
   - Retention: Time-limited with secure deletion protocols

## Implementation Considerations

### Data Processing Pipeline
1. Data extraction from MIMIC
2. Preprocessing for benchmarking tasks
3. Development of test cases
4. Automated validation system
5. Performance metrics calculation

### Privacy and Security Measures
- Data will remain on secure servers
- No protected health information will be published
- Results will be reported in aggregate only
- All team members will sign confidentiality agreements

## Future Directions
- Integration of additional datasets as they become available
- Development of specialized benchmarks for different medical specialties
- Creation of a public leaderboard for medical AI systems
- Contribution back to the research community with benchmarking tools

> [!NOTE]
> This document will be updated with additional benchmarking datasets and protocols as the project progresses. 