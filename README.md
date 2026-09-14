✈️ Airlines Incremental Data Processing Pipeline with CI/CD

An end-to-end Azure Data Engineering project that processes incremental
airline data using Azure Data Factory (ADF) and Azure Data Lake
Storage Gen2 (ADLS Gen2), with source control and automated CI/CD
using GitHub and Azure DevOps.

The project demonstrates a production-style workflow for developing ADF
pipelines in a Development environment, generating deployment artifacts,
and promoting those artifacts to Production.

🏗️ Architecture

                    ┌──────────────────────┐
                    │      ADLS Source      │
                    │   Incremental Data    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       Dev ADF         │
                    │                      │
                    │ Incremental Pipeline │
                    │ Parameterized Flow   │
                    └──────────┬───────────┘
                               │
                         Git Integration
                               │
                               ▼
                    ┌──────────────────────┐
                    │      GitHub Repo      │
                    │      Dev Branch       │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │   Azure DevOps CI    │
                    │                      │
                    │ Build / Validate     │
                    │ Generate ARM Artifact│
                    └──────────┬───────────┘
                               │
                         Build Artifact
                               │
                               ▼
                    ┌──────────────────────┐
                    │ Azure DevOps Release │
                    │       Pipeline       │
                    │                      │
                    │ Environment Config   │
                    │ Production Deploy    │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │       Prod ADF       │
                    │                      │
                    │ Deployed Pipelines  │
                    └──────────┬───────────┘
                               │
                               ▼
                    ┌──────────────────────┐
                    │      Prod ADLS       │
                    │ Landing / Transformed│
                    │        Data          │
                    └──────────────────────┘

🛠️ Tech Stack

Azure Data Lake Storage Gen2 (ADLS Gen2) --- source and target
data storage

Azure Data Factory (ADF) --- orchestration and incremental data
processing

GitHub --- source control and branch-based development

Azure DevOps --- CI/CD automation

ARM Templates --- ADF deployment artifacts

Azure DevOps Agent Pool --- pipeline execution

ADF Parameters --- reusable and environment-aware configuration

🔄 Project Workflow

1. Development

The incremental data processing solution is developed in Azure Data
Factory.

The ADF pipeline reads incremental data from the source ADLS location
and processes it into the target ADLS location using reusable and
parameterized components.

ADLS Source
    ↓
Dev ADF
    ↓
Incremental Processing
    ↓
Dev ADLS Target

2. Version Control

ADF is integrated with GitHub. Development changes are tracked through
the Dev branch.

This provides:

Version history

Change tracking

Branch-based development

Recovery of previous versions

Controlled promotion of changes

3. Continuous Integration

The CI process packages the ADF solution and generates deployment
artifacts.

Dev ADF
   ↓
GitHub / Dev Branch
   ↓
Azure DevOps CI
   ↓
Build & Validation
   ↓
ARM Deployment Artifact

4. Continuous Deployment

The generated artifact is consumed by the Azure DevOps release pipeline
and deployed to the Production ADF environment.

Build Artifact
     ↓
Release Pipeline
     ↓
Production ADF
     ↓
Production ADLS

📸 Implementation Screenshots

Development Repository



Development Pipeline



Development Dataflow



Development Pipeline Run



CI / Artifact Generation



Dev → Production Release



Production Pipeline After Deployment



Production Pipeline Run



Production ADLS Container



Production Landing Zone



Production Transformed Data



📂 Repository Structure

airlines-incremental-data-processing-cicd/
│
├── README.md
│
├── adf/
│   └── README.md
│
└── screenshots/
    ├── dev_repo_branch.png
    ├── creating_dev_dummy_pipeline.png
    ├── dev_pipeline.png
    ├── dev_dataflow.png
    ├── dev_pipeline_run.png
    ├── artifact_release_pipeline.png
    ├── dev_to_prod_release.png
    ├── prod_pipeline_reflects_changes.png
    ├── prod_pipeline_run.png
    ├── prod_container.png
    ├── prod_container_landing_zn.png
    └── prod_container_transform_data_folder.png

🎯 Key Engineering Concepts

Data Engineering

Incremental data processing

ADLS Gen2 storage

Azure Data Factory orchestration

Parameterized pipelines

Reusable pipeline components

Source-to-target data movement

DevOps

Git-based version control

Branch-based development

Azure DevOps CI/CD

Build automation

Artifact generation

ARM template deployment

Release management

Production validation

Environment separation

🚀 Outcome

The project demonstrates a repeatable Azure Data Engineering deployment
workflow in which changes developed in ADF are version-controlled,
packaged into deployment artifacts, and promoted from Development to
Production through Azure DevOps.

Highlights

✅ Incremental data processing

✅ Parameterized ADF pipelines

✅ GitHub source control

✅ Azure DevOps CI pipeline

✅ ADF/ARM artifact generation

✅ Automated Dev → Prod deployment

✅ Production deployment validation

✅ Production ADLS validation

✅ Environment separation

✅ Repeatable deployment workflow

💼 Interview Explanation

I built an incremental airline data processing pipeline using Azure
Data Factory and ADLS Gen2. I integrated ADF with GitHub for version
control and configured Azure DevOps for CI/CD. The CI pipeline
generates deployable ADF artifacts, which are consumed by a release
pipeline to deploy changes into the Production ADF environment. I
validated the deployment by confirming that the updated pipeline was
reflected in Production and that the Production pipeline successfully
processed data into the Production ADLS environment.

🔐 Security

No passwords, access keys, SAS tokens, connection strings, or other
credentials should be committed to this repository.

Environment-specific configuration should be managed through Azure
DevOps variables/variable groups or Azure-native secret management.
