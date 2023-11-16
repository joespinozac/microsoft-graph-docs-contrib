---
title: "Microsoft Graph Data Connect templates"
description: "Make use of templates that are available to help you build Microsoft Graph Data Connect solutions."
author: "rimisra2"
ms.localizationpriority: high
ms.prod: "data-connect"
---

# Microsoft Graph Data Connect templates

Collaboration and communication activities generate a massive amount of rich data in Microsoft 365. You can use Microsoft Graph Data Connect to help you gain insights about your organization. The Data Connect templates help you to reduce the time required to gain data insights and enrich those insights with your own data.

The Microsoft Graph Data Connect templates can help you realize possibilities with your Microsoft 365 data, and accelerate time to added value. Each template contains resources that are specific to different use cases and business scenarios. You can use these templates to help get started with:

- Entity Sentiment Analysis
  - Extract entities from Outlook and Teams data. Then, analyze how users feel about those entities.
  - Sets up Synapse Workspace, Apache Spark Pool, Azure Datalake Storage Account, and Azure Congitive Services resources.
- Organizational Network Analysis
  - Identify collaboration and communication patterns that are key for organizations to achieve real business agility.
  - Sets up Synapse Workspace, Apache Spark Pool, and Azure Datalake Storage Account resources.
- Information Oversharing
  - Secure your business by identifying patterns of information oversharing and fraud in your Microsoft 365 data.
  - Sets up Synapse Workspace, Apache Spark Pool, and Azure Datalake Storage Account resources.

The templates help you quickly provision Azure resources and provide data pipelines and samples that you can use to realize value right away.

To learn more and get started with the Microsoft Graph Data Connect templates, see the [Data Connect solutions GitHub repository](https://github.com/microsoftgraph/dataconnect-solutions/tree/main).

## Quick Start Templates

Quick Start Templates is a feature to help with the setup of the pipelines for extraction MGDC datasets. It enables developers to swiftly generate ARM Templates with a single click, automating the deployment of Azure Data Factory and the pipelines for the datasets. With the Quick Start Templates feature, end users can expedite the setup of essential configurations required for MGDC data extraction, making it more accessible and efficient for developers who have already registered their applications. Currently, the Quick Start Templates only supports Azure Data Factory as the platform and the Copy Activity as the Activity Type. Support for other platforms and activity types will follow.  

### Prerequisites
Following are the pre-requisite steps before using the Quick Start Templates feature. 

- The MGDC application must be configured before using this feature. Refer to the instructions here on how to create an MGDC application.
- The application secret of the Azure Entra application used during MGDC application registration.
- Container in the destination storage account to write data to.
- The Entra application used for the MGDC application should be used to configure the destination linked service. More details about the linked service configuration can be found in the Azure Data Factory documentation.  

### Instructions

1) Developer navigates to Quick Start Templates tab:

2) Open your application from the home page of the MGDC portal extension.

3) Click the start button in the quick start template.

4) Fill in the remaining values in the pre-populated Custom Deployment Form.

- Resource Group: The resource group where your storage account is located. This would be used for the Data Factory location as well.
- Service Principal Id: This is the Entra application used to create an application with MGDC.  This is the pre-populated from the application details.
- Tenant Id: This is the tenant for which data is being extracted. This value would be pre-populated.
- Application Secret: This is the secret for the Entra application used during registration.
- Azure Data Factory Name: There are multiple options for this
  - Pre-populated function: The pre-populated function in the field will automatically generate a new ADF name by appending the unique string associated with the resource group ID to the string "datafactory".
  - Existing Data Factory: Developer could provide an existing data factory in the subscription and resource group provided; this will skip creating a new factory. New pipelines would be added to the existing factory.
  - Custom Data Factory: Developer could provide enter a new unique name for the data factory which would provision a new instance.
- Datasets: These are the datasets in the application for which the pipelines would be generated.
  - One pipeline would be generated per dataset.
  - The value is pre-populated from the application.
- Storage Container: this is the root container in the destination where data will be written to. 

7) Click Review + Create to proceed. A deployment status screen will appear, where the creation of all resources can be monitored.

8) Proceed to trigger the MGDC extraction.

Note: The pipelines do not come configured with the dataset filters. These need to be configured after completing the deployment and before triggering the pipeline. 

9) Configure the data filters for the dataset extractions.

Before triggering the pipeline, click on each Copy Activity to configure the applicable filters to each dataset. For more information about column filters, visit the following documentation: User selection and filtering capabilities in Microsoft Graph Data Connect - Microsoft Graph | Microsoft Learn 
