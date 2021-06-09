---
title: Building Zero Trust ready apps with the Microsoft identity platform
description: Developers have an important role to play in building trustworthy applications that adhere to Zero Trust principles. **Identity** is the backbone of secure app development, acting as the control plane for managing access to your applications to keep users and data safe. This document explains identity best practices for building Zero Trust ready applications using the Microsoft identity platform can help.
ms.date: 04/20/2021
ms.service: security
author: knicholasa
ms.author: nichola
ms.topic: conceptual
---

# Building Zero Trust ready apps with the Microsoft identity platform

:::image type="icon" source="./media/icon-identity-medium.png":::

Traditional approaches to secure application development are no longer enough. Applications are moving into the cloud and their users are working from a variety of devices and locations. Companies want to support employees collaborating with partners who are outside of their organization. At the same time, the threat landscape is evolving constantly, with new exploits and vulnerabilities being disclosed every day.

Identity is the backbone of secure app development, acting as the control plane for managing access to your applications to keep users and data safe. This document explains identity best practices for building Zero Trust ready applications using the Microsoft identity platform.

## What is the Microsoft identity platform?

The Microsoft identity platform is the unification of Microsoft's identity offerings for developers. The platform supports open industry standards. It includes:

- One portal to register all your applications
- One set of Microsoft Authentication libraries for building web, mobile and desktop apps with your favorite framework or programming language
- One endpoint to sign-in any Microsoft identity, which is standards compliant allowing compatibility with third-party libraries.
- Secure access to APIs – from Microsoft Graph to Azure or to your own protected web APIs

The identity platform gives you the ability to authenticate any Microsoft identity including work or school accounts and personal accounts. Your application can also sign in external identities including users from other organizations, social accounts (like Facebook and Google) or sign up with just an email.

The unified platform makes it is even easier to develop for any user and connect every identity to your apps.

> [!VIDEO https://www.youtube.com/embed/uDU1QTSw7Ps]

## IT is rolling out Zero Trust

The implementation of Zero Trust is still evolving, and each organization's journey is unique. But a logical place to start for most customers is identity. The following are some of the polices and controls we see organizations prioritizing as they roll out Zero Trust.

1. **Organizations are restricting user consent to low-risk permissions for publisher verified apps**. IT admins are embracing the principle of verify explicitly by requiring  [publisher verification](/azure/active-directory/develop/publisher-verification-overview), and the principle of least privilege by only allowing user consent for low risk permissions. Before your organization or your customer grants consent, admins will evaluate permissions your app is requesting and the trustworthiness of your app.
1. **Organizations are setting up credential hygiene and rotation policies for apps and services**. If an App's credential gets compromised, the attacker can then acquire tokens under the guise of that app's identity, allowing it to get access to sensitive data, move laterally, and/or establish persistence.
1. **Organizations are rolling out strong auth**. IT administrators expect to be able to set polices requiring multi-factor authentication and passwordless FIDO2 devices.
1. **Organizations are blocking legacy protocols and APIs**. This includes blocking older authentication protocols such as &quot;Basic authentication&quot; and requiring modern protocols like Open ID Connect and OAuth2. Microsoft announced an end of life of June 2022 for Azure AD Graph and the legacy ADAL auth library. Organizations are ensuring applications they depend on are prepared.

## Best practices for developing with Zero Trust

**Use a trusted, standards-based authentication library.** Using a library will save you the time of developing a solution on your own. But more importantly, it will stay up to date and be responsive to the latest technologies and threats. Microsoft has many libraries available including the Microsoft authentication libraries (MSAL), Microsoft.Identity.Web, and the Azure SDK for managed identities. These give you access to features such as conditional access, device registration and management, and the latest innovations such as passwordless and FIDO2 authentication without needing to write any extra code.

**Keep credentials out of your code.** This enables credential rotation by IT administrators without bringing down or redeploying an app. You can use a service such as [Azure Key Vault](/azure/key-vault/general/authentication-fundamentals) or [Azure Managed Identities](/azure/active-directory/managed-identities-azure-resources/overview).

**Design for least privileged access.** This is a key tenet of Zero Trust. You should always provide the least amount of privilege required for the app to do its job. For example, you can use [incremental consent](/azure/active-directory/azuread-dev/azure-ad-endpoint-comparison#incremental-and-dynamic-consent) to only request permissions when they are necessary. Another example is using [granular scopes in Microsoft Graph](/graph/permissions-reference). You can explore scopes using the [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to call an API and examine which permissions are required. They are displayed in order from lowest to highest privilege. Picking the lowest possible privilege will make your application less vulnerable to attacks.

**Support** [**Continuous Access Evaluation (CAE)**](/azure/active-directory/develop/app-resilience-continuous-access-evaluation) **.** CAE allows Microsoft Graph to quickly revoke an active session in response to a security event, for example when a user account is deleted or disabled, MFA is enabled for a user, an administrator explicitly revokes issued tokens for a user, or a user is detected at risk. In addition, when CAE is enabled, tokens issued for Microsoft Graph are valid for 24 hours instead of the standard one hour. This is great for resiliency, as your app can continue to operate without going back to Azure Active Directory for a fresh token every hour.

**Define app roles for IT to assign to users and groups.** [App roles](/azure/active-directory/develop/howto-add-app-roles-in-azure-ad-apps) help your applications implement role-based authorization and security. Common examples of app roles are roles like &quot;Administrator&quot;, &quot;Readers&quot;, and &quot;Contributors&quot;, which allow your application to restrict sensitive actions to users or groups assigned to a role. Using app roles also enables other features such as Azure AD's Privileged Identity Management (PIM) feature, which provide users just-in-time and time-bound access to sensitive roles, reducing the chance of a malicious actor getting that access, or an unauthorized user inadvertently impacting a sensitive resource.

**Become a** [**verified publisher**](/azure/active-directory/develop/publisher-verification-overview). When an application is marked as publisher verified, it means that the publisher has verified their identity using a Microsoft Partner Network account that has completed an established verification process. This is a great for developers of multi-tenant apps, as it helps build trust with IT administrators in customer tenants.

## Next Steps

[Microsoft identity platform documentation](/azure/active-directory/develop/publisher-verification-overview)
