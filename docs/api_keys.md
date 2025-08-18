# OpenAI API Key Best Practices

## Introduction

The OpenAI API structure wasn't immediately apparent until I worked through the documentation.  Here are my notes and some best practices around working with the OpenAI API.

## API Key Safety Basics

There are three core tenets that underpind the practices behind API key safety:
1. Protect the data and the data integrity of your system.
2. Prevent unauthorized use of your API keys.
3. Keep the system available for all users.

In the even of a compromised API Key, your organization could experience the following:
1. Leakage or theft of sensitive data into external systems.
2. Unexpected charges on your OpenAI account.
3. Degradation of service or account restrictions due to bad actors or illegitimate usage of your API account.

### OpenAI Key Types 

OpenAI offers three types of keys:
1. Admin Keys
2. Project Keys
3. Individual Keys

Let's talk about the differences between these key types and the best practices around them.

#### Admin Keys

Admin Keys can only be accessed by Organizational owners and their scope is limitede to the [OpenAI Admin API](https://help.openai.com/en/articles/9687866-admin-and-audit-logs-api-for-the-api-platform) which provides the ability to programatically manage users, projects, and billing.

These keys are non-recoverable.  If an Admin Key is lost or compromised, it must be deleted and a new key created.

Since Admin keys have the ability to create API keys and users, it is critical to always assign least privilege, rotate keys regularly, and monitor usage closely.

### Project Keys

Project Keys are scoped to a specific project within an organization.  These keys can be created directly or created via a service account.

Project Keys are limited in scope to only interact with resources within a given project and also are constrained to the resources of that project.

### Individual Keys (Legacy - DO NOT USE)

Individual api keys are keys issued and scoped to a single individual.  The individual API Key provides API access to every organization and project that the user belongs to.

Because the individual API key has such broad cross organization and cross project access, **OpenAI actively discourages the use of this API key**.  The availabilty of this key is soley for the support of legacy applications.

According to the [OpenAI API Key Best Practices](https://help.openai.com/en/articles/5112595-best-practices-for-api-key-safety) and the [OpenAI Terms of Service](https://beta.openai.com/terms-of-use), individual API keys **CANNOT BE SHARED BETWEEN USERS.**  

### OpenAI Best Practices

#### Monitor Key Usage
Organizational owners can monitor the usage of all individual keys and project keys within their organization from the [Usage Dashboard](https://platform.openai.com/settings/organization/usage).

Monitoring key usage is key to detecting authorized or improper use of the API keys.

#### Project Keys with Limited Scope and Budget
Any shared application should leverage a project key.  These keys should be created with a limited scope and limited budget to prevent unexpected charges or API disruption in the event of a leaked key.

Project API keys should be used when experimenting or spiking functionality out within a project.

#### Use Service Accounts for project deployments
OpenAI recommends the creation of "Service Accounts" to facilitate machine to machine API usage instead of creating raw API keys within a project.  These accounts represent a non-human user.  These accounts are listed in line with the other users on the project and are provided a unique API key for accessing the system.

Service accounts should be used for any deployed or production system that requires strict auditing and tracking of API usage.


### Common API Safety Best Practices

#### Least Privilege

Users and API keys should be assigned the minimum level of access required to perform their function.  This limits the potential damage in the event of a compromised key.

#### Regular Rotation

API keys should be rotated regularly to minimize the risk of long-term exposure.  A regular rotation schedule should be established and followed.

#### Secure Storage

API keys should be stored securely using environment variables or secret management tools.  Keys should never be hardcoded in source code or exposed in public repositories.

Organizations should consider using a key management system (KMS) to securely store and manage API keys on behalf of their users.

#### Monitoring and Auditing

Regularly monitor API key usage for any unusual or unauthorized activity.  Set up alerts for suspicious behavior and conduct periodic audits of API key access and usage.


### Common API Key Misuse

#### Hardcoding Keys

Hardcoding API keys in source code or configuration files can lead to accidental exposure, especially if the code is shared publicly or with third parties.

#### Sharing Keys

Sharing API keys between users or applications increases the risk of unauthorized access and makes it difficult to track usage.

#### Client Side Exposure

Exposing API keys in client-side code (e.g., JavaScript running in a web browser) can lead to easy extraction by malicious actors.  This also includes embedding keys in mobile applications or desktop applications where they can be decompiled and API KEY extracted.

