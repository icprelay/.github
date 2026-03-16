# ICP Relay 

ICP Relay is a cloud-native data delivery platform that enables SaaS vendors to provide reliable data integrations to their customers without building custom integration projects.

Instead of implementing one-off integrations for every customer, ICP Relay allows vendors to publish **reusable integration workflows** that customers activate as **configurable integration instances**.

The platform receives **webhooks from the SaaS application** and delivers the data to external systems such as SQL databases, REST APIs, Microsoft Teams, SharePoint, or other endpoints.

## Why ICP Exists

Many B2B SaaS products face the same problem:

- Customers need their data exprted to external systems
- Integrations are implemented as **custom projects**
- Backlogs grow and engineering teams become bottlenecks

ICP Relay converts these integrations from **projects into configurable products**.

## Architecture overview
```
SaaS Platform
     │
     │ Webhook or a scheduled api call
     ▼
ICP Relay Ingest Workflow
(Azure Logic Apps)
     │
     ▼
ICP Relay API fan-out
(Azure App Service)
     │
     ▼
Integration Workflows
(Azure Logic Apps)
     │
     ▼
External Targets
SQL | REST | Teams | SharePoint | BI | SMS | Blob | and more...
```

Each integration runs as a **customer-scoped integration** instance with its own configuration and secrets.

## Repositories

ICP Relay is split into three repositories

### `icp-core`

Core platform implementation.

Contains:
- ui
- api
- domain models
- router workflow
- example workflows for ingest and targets

This repository contains the **core runtime logic of the platform**.

### `icp-schemas`

Versioned schemas used by the workflows.

Includes:
- stored event schema
- canonical event schema
- record data schema

This repository ensures **stable contracts between SaaS events and integrations**.

### `icp-deploy`

Infrastructure and deployment automation for Azure DevOps

Contains:

- infrastructure definitions (bicep)
- infrastructure & deployment pipelines (yaml)
- sql pipeline for running migrations, seeding, and grants.
- release workflows that pull tagged versions from `icp-core`

This repository manages **environment provisioning and releases**.

### Project Status

ICP Relay is under active development and is designed for deployent in **customer-owned Azure environments** (SaaS vendors).