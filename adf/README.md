Azure Data Factory Implementation

This directory documents the Azure Data Factory portion of the
Airlines Incremental Data Processing project.

ADF is responsible for orchestrating the movement and processing of
incremental airline data between ADLS Gen2 locations.

🏗️ ADF Architecture

ADLS Source
    │
    ▼
┌─────────────────────────┐
│       Azure Data        │
│        Factory          │
│                         │
│ Parameterized Pipeline  │
│         │               │
│         ▼               │
│ Incremental Processing  │
│         │               │
│         ▼               │
│ Data Transformation     │
└─────────┬───────────────┘
          │
          ▼
     ADLS Target

🔹 Development Pipeline

The pipeline was developed in the Dev ADF environment and designed to
process incremental data from ADLS.

The solution uses parameters to make paths and processing components
reusable rather than hard-coding every environment-specific value.

Main responsibilities

Read source data from ADLS

Process incremental data

Apply the required data movement/transformation logic

Write processed data to the target ADLS location

Support reusable parameterized execution

🔹 Parameterization

Parameterization is used to make the ADF solution reusable across
environments.

Typical values that can be parameterized include:

Source container
Source folder
Target container
Target folder
File/path information
Environment-specific resources

This allows the same logical pipeline design to be deployed without
rebuilding the pipeline separately for Development and Production.

🔹 Incremental Processing

The pipeline is designed around incremental processing so that new or
changed source data can be processed without unnecessarily reprocessing
the complete historical dataset.

Conceptually:

Existing Data
     │
     ├───────────────┐
     │               │
     ▼               ▼
Already Processed   New Incremental Data
                         │
                         ▼
                  ADF Processing
                         │
                         ▼
                  Target ADLS

The exact incremental logic and parameters should be kept in the ADF
implementation rather than duplicated in documentation.

🔹 Git Integration

The Dev ADF environment is connected to GitHub.

The development workflow is:

ADF Development
      ↓
Git Changes
      ↓
Dev Branch
      ↓
Publish
      ↓
Azure DevOps CI/CD

This provides version history and allows ADF changes to be tracked
before deployment.

🔹 CI/CD Deployment

ADF deployment is separated into two major stages.

Continuous Integration

The CI pipeline:

Retrieves the ADF source/configuration

Validates/builds the solution

Generates deployable ADF/ARM artifacts

Publishes the artifact for the release stage

GitHub
  ↓
CI Pipeline
  ↓
Validation / Build
  ↓
ARM Artifact

Continuous Deployment

The release pipeline consumes the generated artifact and deploys it to
the Production ADF environment.

ARM Artifact
     ↓
Release Pipeline
     ↓
Production ADF

Environment-specific configuration is supplied through the deployment
configuration/variables.

🔹 Development to Production Flow

┌──────────────┐
│   Dev ADF    │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ GitHub Dev   │
│    Branch    │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Azure DevOps │
│     CI       │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Build/ARM    │
│   Artifact   │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│ Azure DevOps │
│    Release   │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Prod ADF   │
└──────┬───────┘
       │
       ▼
┌──────────────┐
│   Prod ADLS  │
└──────────────┘

📸 ADF Screenshots

The main ADF evidence is available in the repository's screenshots/
directory.

Recommended evidence:

dev_pipeline.png --- Development ADF pipeline

dev_dataflow.png --- Development dataflow

dev_pipeline_run.png --- Successful Development execution

prod_pipeline_reflects_changes.png --- Production pipeline after
deployment

prod_pipeline_run.png --- Successful Production execution

🎯 ADF Engineering Concepts Demonstrated

Azure Data Factory orchestration

ADLS Gen2 integration

Incremental data processing

Pipeline parameterization

Reusable data processing design

Git integration

ARM-based deployment

Environment separation

CI/CD deployment through Azure DevOps

🔐 Security

Do not commit:

Storage account keys

SAS tokens

Passwords

Connection strings

Client secrets

Service principal secrets

Use Azure DevOps variables/variable groups and Azure-native secret
management for sensitive configuration.

💼 Interview Summary

I used Azure Data Factory to build a parameterized incremental data
processing pipeline over ADLS Gen2. The Dev ADF environment was
integrated with GitHub for version control. I then configured Azure
DevOps CI/CD so that ADF changes are packaged into deployment
artifacts and promoted to Production through a release pipeline.
Finally, I validated the deployed Production pipeline and its ADLS
output.
