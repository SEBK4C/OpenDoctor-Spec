# Data Sources

## Overview
This document outlines authoritative medical data sources for knowledge panels and dictionary data for the Open Doctor project. These sources have been selected based on their reliability, comprehensiveness, and accessibility.

## Primary Medical Data Sources

### National Library of Medicine (NLM)
**Website**: [NLM](https://www.nlm.nih.gov/)  
**Access**: Public access with registration for certain resources  
**Description**: The world's largest biomedical library, providing extensive resources including PubMed, MedlinePlus, and TOXNET.

**Key Resources**:
- **PubMed**: Database of biomedical literature
- **MedlinePlus**: Consumer health information
- **ClinicalTrials.gov**: Database of clinical studies
- **Genetics Home Reference**: Genetic condition information

### Centers for Disease Control and Prevention (CDC)
**Website**: [CDC](https://www.cdc.gov/)  
**Access**: Public  
**Description**: Official source for health information in the United States, providing epidemiological data, prevention guidelines, and health statistics.

**Key Resources**:
- **Morbidity and Mortality Weekly Report (MMWR)**: Updates on disease trends
- **CDC Wonder**: Data query system for public health information
- **Growth Charts**: Reference data for pediatric development
- **Vaccine Information Statements**: Standard information about immunizations

### World Health Organization (WHO)
**Website**: [WHO](https://www.who.int/)  
**Access**: Public  
**Description**: Global authority directing international health within the United Nations system, offering worldwide health data and standards.

**Key Resources**:
- **International Classification of Diseases (ICD)**: Standard diagnostic tool
- **Global Health Observatory**: Worldwide health statistics
- **Essential Medicines List**: Core medications needed for healthcare systems
- **Technical guidance documents**: Standards for healthcare practices

### National Institute of Health (NIH)
**Website**: [NIH](https://www.nih.gov/)  
**Access**: Public with registration for certain datasets  
**Description**: US medical research agency composed of 27 Institutes and Centers, each focused on particular diseases or body systems.

**Key Resources**:
- **Clinical guidelines**: Evidence-based treatment recommendations
- **Health Information**: Condition-specific resources
- **Research resources**: Biomedical research databases
- **Genetic and rare diseases information**: Specialized information on genetic conditions

## Specialized Data Sources

### Mayo Clinic
**Website**: [Mayo Clinic](https://www.mayoclinic.org/)  
**Access**: Public  
**Description**: Nonprofit organization committed to clinical practice, education, and research, providing detailed information on diseases and conditions.

**Key Resources**:
- **Diseases and Conditions**: Comprehensive patient education
- **Symptoms**: Detailed symptom information
- **Tests and procedures**: Medical test information
- **Drugs and supplements**: Medication information

### Cleveland Clinic
**Website**: [Cleveland Clinic](https://my.clevelandclinic.org/)  
**Access**: Public  
**Description**: Nonprofit multispecialty academic medical center that integrates clinical and hospital care with research and education.

**Key Resources**:
- **Health Library**: Comprehensive health information
- **Disease management guides**: Condition-specific care guidelines
- **Treatment guides**: Procedure information
- **Health tools and calculators**: Interactive health assessment tools

## Academic and Research Sources

### PubMed Central (PMC)
**Website**: [PMC](https://www.ncbi.nlm.nih.gov/pmc/)  
**Access**: Public  
**Description**: Free digital repository of full-text biomedical and life sciences journal literature at the U.S. National Institutes of Health.

### Cochrane Library
**Website**: [Cochrane Library](https://www.cochranelibrary.com/)  
**Access**: Some content requires subscription  
**Description**: Collection of databases containing high-quality, independent evidence to inform healthcare decision-making.

## Implementation Guidelines

### Data Integration Priority
1. National Library of Medicine resources
2. CDC clinical guidelines
3. WHO standards and classifications
4. NIH specialized research databases
5. Academic sources for deeper clinical insights

### Usage Considerations
- Implement regular update processes to maintain current medical information
- Provide clear attribution and source information for all data
- Establish verification protocols for critical medical information
- Develop a system to handle conflicting information from different sources

### Technical Integration
- Establish API connections where available
- Implement scheduled data scraping with appropriate permissions
- Create data transformation pipelines to standardize information format
- Develop versioning systems to track changes in medical recommendations

## Future Data Sources
- Electronic Health Record (EHR) anonymized datasets
- Patient-reported outcomes databases
- Genomic and precision medicine databases
- Medical imaging repositories
- Pharmacovigilance databases

> [!NOTE]
> This document will be updated as additional data sources are evaluated and integrated into the Open Doctor system.

> [!IMPORTANT]
> All data usage must comply with relevant licensing terms, privacy regulations, and attribution requirements. 