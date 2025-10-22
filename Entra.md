
```markdown
# Secure Access with Azure Active Directory (Azure AD)

A hands-on implementation of secure identity and access management using Azure Active Directory. This project covers cloud and hybrid identity, user and group management, multi-factor authentication (MFA), passwordless options, and hybrid connectivity via Azure AD Connect. It emphasizes RBAC, SSO, conditional access, and security best practices for modern cloud-first environments.

## Overview

- Focus: Identity and access management using Azure AD and Entra platform evolution
- Scope: Cloud and hybrid identity, user/group management, MFA/passwordless, Azure AD Connect (hybrid identity), conditional access, and app access management
- Audience: Security engineers, IT admins, and cloud architects exploring Azure AD capabilities

## Learning Outcomes

- Explain Azure AD and Azure AD Domain Services features, licensing, and how they compare to traditional Active Directory.
- Create and manage users, groups, and administrative units in cloud and hybrid contexts; configure administrative units for scoped administration.
- Describe authentication and password protection options in Azure AD; configure and implement MFA (including passwordless methods) and risk-based access controls.
- Deploy and configure Azure AD Connect to establish a hybrid identity solution; enable pass-through authentication and federation, with password writeback as appropriate.
- Manage application access and implement security policies (e.g., conditional access) to protect resources.
- Understand the role of Azure AD in RBAC, SSO, identity provisioning, and cloud security.

## Project Scope & Modules

### Module 1: Managing users in Microsoft Entra Directory (Azure AD)

- Explore Azure AD fundamentals, licensing, and feature comparisons with on-premises AD DS.
- Create, update, and deactivate users; assign licenses; configure basic permissions.
- Manage groups and administrative units to control scope and governance.
- Enable external collaboration and guest access to resources.

### Module 2: Managing secure access

- Understand authentication and authorization flows for Azure AD.
- Implement password protection and MFA strategies, including passwordless options.
- Plan and deploy MFA (e.g., OATH tokens, phone-based prompts) and perform testing.
- Deploy Azure AD Connect to enable hybrid identity, with options for pass-through authentication and federation.
- Implement password writeback and cloud-based self-service password reset to on-premises environments.

### Module 3: Course project

- Practice creating and managing users, groups, and administrative units.
- Implement authentication methods (MFA, passwordless) and conditional access policies.
- Deploy and configure Azure AD Connect for hybrid identity; validate synchronization and authentication flows.
- Manage application access and resource provisioning; apply security policies and RBAC for differentiated access.
- Document project decisions, configurations, and test results.

## Key Technologies & Concepts Demonstrated

- Azure Active Directory (Azure AD), Entra platform evolution
- Azure AD Connect (hybrid identity) and hybrid identity scenarios
- Identity provisioning, RBAC, and administrative units
- Authentication methods: MFA, passwordless, pass-through authentication, federation
- Password protection, password writeback, cloud self-service password reset
- Conditional Access and SSO across cloud and on-prem apps
- External collaboration (guest users) and app access management
- Secure access patterns for cloud-first and hybrid environments

## Implementation Highlights

- Built and organized an Azure AD tenant; created users and groups; assigned licenses.
- Created administrative units to delegate governance and control access boundaries.
- Configured MFA options (e.g., Microsoft Authenticator, OATH tokens) and tested user enrollment.
- Enabled and validated passwordless authentication methods for eligible users.
- Planned and deployed Azure AD Connect; configured synchronization, user sign-in, and password writeback as appropriate.
- Set up conditional access policies to enforce policy-based access (location, device compliance, risk signals).
- Configured application registrations and enterprise applications; assigned RBAC-based access to resources.
- Verified hybrid login scenarios, including SSO for cloud and on-prem apps; validated failover/fallback paths.
- Documented decisions, tested scenarios, and captured metrics for security posture improvements.

## Outcomes & Impact (Examples)

- Reduced administrative overhead by delegating governance via administrative units.
- Improved security posture with MFA enforcement and conditional access policies.
- Achieved seamless SSO across multiple cloud apps and on-prem resources.
- Enabled hybrid identity with Azure AD Connect, enabling secure sign-ins and password writeback.
- Enhanced user experience with passwordless authentication options and self-service capabilities.

## What I Learned & Key Takeaways

- Azure AD vs. on-prem AD DS: strengths, limitations, and how they fit in hybrid environments.
- The importance of administrative boundaries (administrative units) to minimize blast radius and simplify governance.
- Balancing security and usability with MFA, conditional access, and passwordless strategies.
- Practical considerations for hybrid identity: syncing vs. federation, authentication flow choices, and monitoring.
- How to plan, test, and document authentication and provisioning workflows for a production-like environment.

## How to Present this in Your Portfolio (GitHub README)

- Include a concise project summary at the top.
- List modules and skills gained as bullet points.
- Provide implementation highlights with concrete actions you performed.
- Add an outcomes/impact section with measurable results (even qualitative).
- Attach or link artifacts: architecture diagram, sample conditional access policy, a screenshot of Azure AD Connect configuration, or a sample code snippet (see code blocks below).
- Include lessons learned and next steps for further learning or improvements.

## Example Code Snippets

- PowerShell: create a new user and assign a license (adjust with your tenant details)
```powershell
# Connect to MS Graph or Azure AD module
Connect-AzureAD

# Create a new user
$pwd = (ConvertTo-SecureString "P@ssw0rd123!" -AsPlainText -Force)
New-AzureADUser -DisplayName "Alex Doe" -UserPrincipalName "alex.doe@contoso.onmicrosoft.com" -AccountEnabled $true -PasswordProfile (New-Object -TypeName Microsoft.Open.AzureAD.Model.PasswordProfile -Property @{Password=$pwd; ForceChangePasswordNextLogin=$true})

# Assign a license (requires a license SKU, replace with your SKU)
$skuId = (Get-AzureADSubscribedSku | Where-Object { $_.SkuPartNumber -eq "ENTERPRISEPACK" }).SkuId
Set-AzureADUserLicense -ObjectId (Get-AzureADUser -SearchString "alex.doe@contoso.onmicrosoft.com").ObjectId -AddLicenses $skuId -ReleaseLicenses $null
```

```
