# Secure access for workload identities

A workload identity is an identity used by a software workload (such as an application, service, script, or container) to authenticate and access other services and resources. The terminology is inconsistent across the industry, but generally a workload identity is something you need for your software entity to authenticate with some system. For example, a workload identity could be a user account that your client authenticates as to access a MongoDB database. A workload identity could also be an AWS service role attached to an EC2 instance with read-only access to an Amazon S3 bucket.

In Microsoft Entra ID, workload identities are applications, service principals, and managed identities.

An application is an abstract entity, or template, defined by its application object. The application object is the global representation of your application for use across all tenants. The application object describes how tokens are issued, the resources the application needs to access, and the actions that the application can take.

A service principal is the local representation, or application instance, of a global application object in a specific tenant. An application object is used as a template to create a service principal object in every tenant where the application is used. The service principal object defines what the app can actually do in a specific tenant, who can access the app, and what resources the app can access.

A managed identity is a special type of service principal that eliminates the need for developers to manage credentials.

Here are some ways that workload identities in Microsoft Entra ID are used:

1) An app that enables a web app to access Microsoft Graph based on admin or user consent. This access could be either on behalf of the user or on behalf of the application.

2) A managed identity used by a developer to provision their service with access to an Azure resource such as Azure Key Vault or Azure Storage.

3) A service principal used by a developer to enable a CI/CD pipeline to deploy a web app from GitHub to Azure App Service.

## Workload identities, other machine identities, and human identities

At a high level, there are two types of identities: human and machine/non-human identities. Workload identities and device identities together make up a group called machine (or non-human) identities. Workload identities represent software workloads while device identities represent devices such as desktop computers, mobile, IoT sensors, and IoT managed devices. Machine identities are distinct from human identities, which represent people such as employees (internal workers and front line workers) and external users (customers, consultants, vendors, and partners).

![image](https://github.com/user-attachments/assets/3a585001-15b8-475d-ae2d-d7702e4b8a1a)

