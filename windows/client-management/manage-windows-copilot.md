---
title: Manage Copilot in Windows
description: Learn how to manage Copilot in Windows for commercial environments using MDM and group policy. Learn about the chat providers available to Copilot in Windows.
ms.topic: conceptual
ms.subservice: windows-copilot
ms.date: 01/22/2024
ms.author: mstewart
author: mestew
appliesto:
- ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11, version 22H2 or later</a>
---

# Manage Copilot in Windows
<!--8445848-->

>**Looking for consumer information?** See [Welcome to Copilot in Windows](https://support.microsoft.com/windows/welcome-to-copilot-in-windows-675708af-8c16-4675-afeb-85a5a476ccb0).

Copilot in Windows provides centralized generative AI assistance to your users right from the Windows desktop. Copilot in Windows appears as a side bar docked on the Windows desktop and is designed to help users get things done in Windows. Copilot in Windows can perform common tasks in Windows like changing Windows settings, which makes it different from the browser-based [Copilot in Edge](/copilot/edge). However, both user experiences, Copilot in Windows and Copilot in Edge, can share the same underlying chat provider platform. It's important for organizations to properly configure the chat provider platform that Copilot in Windows uses, since it's possible for users to copy and paste sensitive information into the chat.

> [!Note]
> - Copilot in Windows is currently available as a preview. We will continue to experiment with new ideas and methods using your feedback.
> - Copilot in Windows is being released in preview to select global markets as part of our latest update to Windows 11. The initial markets for the Copilot in Windows preview include North America and parts of Asia and South America. It is our intention to add additional markets over time.

## Configure Copilot in Windows for commercial environments

At a high level, managing and configuring Copilot in Windows for your organization involves the following steps:

1. Understand the [available chat provider platforms for Copilot in Windows](#chat-provider-platforms-for-copilot-in-windows)
1. [Configure the chat provider platform](#configure-the-chat-provider-platform-that-copilot-in-windows-uses) used by Copilot in Windows
1. Ensure the [Copilot in Windows user experience](#ensure-the-copilot-in-windows-user-experience-is-enabled) is enabled
1. Verify [other settings that might affect Copilot in Windows](#other-settings-that-might-affect-copilot-in-windows-and-its-underlying-chat-provider) and its underlying chat provider

Organizations that aren't ready to use Copilot in Windows can disable it until they're ready with the **Turn off Windows Copilot** policy. This policy setting allows you to turn off Copilot in Windows. If you enable this policy setting, users can't use Copilot in Windows and the icon doesn't appear on the taskbar either. If you disable or don't configure this policy setting, users can use Copilot in Windows when it's available to them.

| &nbsp; | Setting  |
|---|---|
| **CSP** | ./User/Vendor/MSFT/Policy/Config/WindowsAI/[TurnOffWindowsCopilot](mdm/policy-csp-windowsai.md#turnoffwindowscopilot) |
| **Group policy** | User Configuration > Administrative Templates > Windows Components > Windows Copilot > **Turn off Windows Copilot** |


## Chat provider platforms for Copilot in Windows

Copilot in Windows can use either Microsoft Copilot or Copilot with commercial data protection as its chat provider platform. The chat provider platform is the underlying service that Copilot in Windows uses to communicate with the user. The chat provider platform is important because it's possible for users to copy and paste sensitive information into the chat. Each chat provider platform has different privacy and security protections.

### Copilot

Copilot is a consumer experience and has a daily limit on the number of chat queries per user when not signed in with a Microsoft account. It doesn't offer the same data protection as Copilot with commercial data protection.

- [Copilot in Windows: Your data and privacy](https://support.microsoft.com/windows/3e265e82-fc76-4d0a-afc0-4a0de528b73a)
- The privacy statement for using Copilot follows the [Microsoft privacy statement](https://privacy.microsoft.com/privacystatement) including the product specific guidance in the Microsoft privacy statement for **Bing** under the **Search, Microsoft Edge, and artificial intelligence** section.


### Copilot with commercial data protection

[Copilot with commercial data protection](/copilot/overview) is intended for commercial use scenarios and offers commercial data protection. The following privacy and security protections apply for Copilot with commercial data protection:

- User and organizational data is protected, chat data isn't saved, and your data isn't used to train the underlying large language models. Because of this protection, chat history, 3rd-party plugins, and the Bing app for iOS or Android aren't currently supported. Copilot with commercial data protection is accessible from mobile browsers, including Edge mobile on iOS and Android. Review the Copilot with commercial data protection [privacy statement](/copilot/privacy-and-protections).
- Copilot with commercial data protection is available, at no additional cost, for the following licenses:
   - Microsoft 365 E3 or E5
   - Microsoft 365 A3 or A5 for faculty
   - Microsoft 365 Business Standard
   - Microsoft 365 Business Premium

  > [!Note]
  > Copilot doesn't have access to Microsoft 365 Apps data, such as email, calendar, or files using Microsoft Graph, unlike [Copilot for Microsoft 365](/microsoft-365-copilot/microsoft-365-copilot-overview) which can be used in the Microsoft 365 apps.

## Configure the chat provider platform that Copilot in Windows uses

Configuring the correct chat provider platform for Copilot in Windows is important because it's possible for users to copy and paste sensitive information into the chat. Each chat provider platform has different privacy and security protections. Once you select the chat provider platform that you want to use for Copilot in Windows, ensure it's configured for your organization's users. The following sections describe how to configure the chat provider platform that Copilot in Windows uses.

### Microsoft Copilot as the chat provider platform

Copilot is used as the default chat provider platform for Copilot in Windows when any of the following conditions occur:

- Commercial data protection isn't configured for the user.
- Commercial data protection is [turned off](/copilot/manage).
- The user isn't assigned a license that includes Copilot with commercial data protection.
- The user isn't signed in with a Microsoft Entra account that's licensed for Copilot with commercial data protection.

### Copilot with commercial data protection as the chat provider platform (recommended for commercial environments)

To verify that Copilot with commercial data protection is enabled for the user as the chat provider platform for Copilot in Windows, use the following instructions:

1. Sign into the [Microsoft 365 admin center](https://admin.microsoft.com/).
1. In the admin center, select  **Users** > **Active users** and verify that users are assigned a license that includes **Copilot**. Copilot with commercial data protection is included and enabled by default for users that are assigned one of the following licenses:
   - Microsoft 365 E3 or E5
   - Microsoft 365 A3 or A5 for faculty
     - Currently, Microsoft 365 A3 and A5 for faculty requires additional configuration. For more information, see [Manage Copilot](/copilot/manage).
   - Microsoft 365 Business Standard
   - Microsoft 365 Business Premium
1. To verify that commercial data protection is enabled for the user, select the user's **Display name** to open the flyout menu.
1. In the flyout, select the **Licenses & apps** tab, then expand the **Apps** list.
1. Verify that **Copilot** is enabled for the user.
1. If you prefer to view a user's licenses from the [Azure portal](https://portal.azure.com), you'll find it under **Microsoft Entra ID** > **Users**. Select the user's name, then **Licenses**. Select a  license that includes **Copilot**, and verify that it's listed as **On**.

   > [!Note]
   > If you previously disabled Copilot with commercial data protection (formerly Bing Chat Enterprise) using the URL, `https://aka.ms/TurnOffBCE`, see [Manage Copilot](/copilot/manage) for verifying that commercial data protection is enabled for your users.

The following sample PowerShell script connects to Microsoft Graph and lists which users that have Copilot with commercial data protection enabled and disabled:

```powershell
# Install Microsoft Graph module
if (-not (Get-Module Microsoft.Graph.Users)) {
    Install-Module Microsoft.Graph.Users
}

# Connect to Microsoft Graph
Connect-MgGraph -Scopes 'User.Read.All'

# Get all users
$users = Get-MgUser -All -ConsistencyLevel eventual -Property Id, DisplayName, Mail, UserPrincipalName, AssignedPlans

# Users with Copilot with commercial data protection enabled
$users | Where-Object { $_.AssignedPlans -and $_.AssignedPlans.Service -eq "Bing" -and $_.AssignedPlans.CapabilityStatus -eq "Enabled" } | Format-Table

# Users without Copilot with commercial data protection enabled
$users | Where-Object { -not $_.AssignedPlans -or ($_.AssignedPlans.Service -eq "Bing" -and $_.AssignedPlans.CapabilityStatus -ne "Enabled") } | Format-Table
```

When Copilot with commercial data protection is the chat provider platform, the user experience clearly states that **Your personal and company data are protected in this chat**. There's also a shield symbol labeled **Protected** at the top of the Copilot in Windows sidebar and the provider is listed under the Copilot logo when the sidebar is first opened. The following image shows the message that's displayed in this scenario:

:::image type="content" source="images/bing-chat-enterprise-chat-provider.png" alt-text="Screenshot of the Copilot in Windows user experience when Copilot with commercial data protection is the chat provider." lightbox="images/bing-chat-enterprise-chat-provider.png":::

## Ensure the Copilot in Windows user experience is enabled

Once you've configured the chat provider platform that Copilot in Windows uses, you need to ensure that the Copilot in Windows user experience is enabled. Ensuring the Copilot in Windows user experience is enabled varies by the Windows version.

### Enable the Copilot in Windows user experience for Windows 11, version 22H2 clients

Copilot in Windows isn't technically enabled by default for managed Windows 11, version 22H2 devices because it's behind a [temporary enterprise control](/windows/whats-new/temporary-enterprise-feature-control). For the purposes of temporary enterprise control, a system is considered managed if it's configured to get updates from Windows Update for Business or [Windows Server Update Services (WSUS)](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus). Clients that get updates from Microsoft Configuration Manager, Microsoft Intune, and Windows Autopatch are considered managed since their updates ultimately come from WSUS or Windows Updates for Business.

To enable Copilot in Windows for managed Windows 11, version 22H2 devices, you need to enable features under temporary enterprise control for these devices. Since enabling features behind [temporary enterprise control](/windows/whats-new/temporary-enterprise-feature-control) can be impactful, you should test this change before deploying it broadly. To enable Copilot in Windows for managed Windows 11, version 22H2 devices, use the following instructions:

1. Verify that the user accounts have the correct chat provider platform configured for Copilot in Windows. For more information, see the [Configure the chat provider platform that Copilot in Windows uses](#configure-the-chat-provider-platform-that-copilot-in-windows-uses) section.
1. Apply a policy to enable features under temporary enterprise control for managed clients. The following polices apply to Windows 11, version 22H2 with [KB5022845](https://support.microsoft.com/topic/february-14-2023-kb5022845-os-build-22621-1265-90a807f4-d2e8-486e-8a43-d09e66319f38) and later:
   - **Group Policy:** Computer Configuration\Administrative Templates\Windows Components\Windows Update\Manage end user experience\\**Enable features introduced via servicing that are off by default**

    - **CSP**: ./Device/Vendor/MSFT/Policy/Config/Update/[AllowTemporaryEnterpriseFeatureControl](/windows/client-management/mdm/policy-csp-update?toc=/windows/deployment/toc.json&bc=/windows/deployment/breadcrumb/toc.json#allowtemporaryenterprisefeaturecontrol)
       - In the Intune [settings catalog](/mem/intune/configuration/settings-catalog), this setting is named **Allow Temporary Enterprise Feature Control** under the **Windows Update for Business** category.
     > [!Important]
     > For the purposes of temporary enterprise control, a system is considered managed if it's configured to get updates from Windows Update for Business or [Windows Server Update Services (WSUS)](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus). Clients that get updates from Microsoft Configuration Manager, Microsoft Intune, and Windows Autopatch are considered managed since their updates ultimately come from WSUS or Windows Updates for Business.

1. Copilot in Windows will be initially deployed to devices using a controlled feature rollout (CFR). Depending on how soon you start deploying Copilot in Windows, you might also need to [enable optional updates](/windows/deployment/update/waas-configure-wufb#enable-optional-updates) with one of the following policies:
   - **Group Policy:** Computer Configuration\Administrative Templates\Windows Components\Windows Update\Windows Update for Business\\**Allow updates to Windows optional features**
   - **CSP**: ./Device/Vendor/MSFT/Policy/Config/Update/[AllowOptionalUpdates](/windows/client-management/mdm/policy-csp-update?toc=/windows/deployment/toc.json&bc=/windows/deployment/breadcrumb/toc.json#allowoptionalupdates)
      - In the Intune [settings catalog](/mem/intune/configuration/settings-catalog), this setting is named **Allow optional updates** under the **Windows Update for Business** category.

   The optional updates policy applies to Windows 11, version 22H2 with [KB5029351](https://support.microsoft.com/help/5029351) and later. When setting policy for [optional updates](/windows/deployment/update/waas-configure-wufb#enable-optional-updates), ensure you select one of the following options that includes CFRs:
    - Automatically receive optional updates (including CFRs)
      - This selection places devices into an early CFR phase
    - Users can select which optional updates to receive

1. Windows 11, version 22H2 devices display Copilot in Windows when the CFR is enabled for the device. CFRs are enabled for devices in phases, sometimes called waves.

### Enable the Copilot in Windows user experience for Windows 11, version 23H2 clients

Once a managed device installs the version 23H2 update, the [temporary enterprise control](/windows/whats-new/temporary-enterprise-feature-control) for Copilot in Windows is removed. This means that Copilot in Windows is enabled by default for these devices.

While the user experience for Copilot in Windows is enabled by default, you still need to verify that the correct chat provider platform configured for Copilot in Windows. While every effort is made to ensure that Copilot with commercial data protection is the default chat provider for commercial organizations, it's still possible that Copilot might still be used if the configuration is incorrect, or if other settings are affecting Copilot in Windows. For more information, see:
- [Configure the chat provider platform that Copilot in Windows uses](#configure-the-chat-provider-platform-that-copilot-in-windows-uses)
- [Other settings that might affect Copilot in Windows and its underlying chat provider](#other-settings-that-might-affect-copilot-in-windows-and-its-underlying-chat-provider)

Organizations that aren't ready to use Copilot in Windows can disable it until they're ready by using the following policy:

- **CSP**: ./User/Vendor/MSFT/Policy/Config/WindowsAI/[TurnOffWindowsCopilot](mdm/policy-csp-windowsai.md#turnoffwindowscopilot)
- **Group Policy**: User Configuration\Administrative Templates\Windows Components\Windows Copilot\\**Turn off Windows Copilot**

## Other settings that might affect Copilot in Windows and its underlying chat provider

Copilot in Windows and [Copilot in Edge](/copilot/edge), can share the same underlying chat provider platform. This also means that some settings that affect Copilot, Copilot with commercial data protection, and Copilot in Edge can also affect Copilot in Windows. The following common settings might affect Copilot in Windows and its underlying chat provider:

### Bing settings

- If [SafeSearch](https://support.microsoft.com/topic/946059ed-992b-46a0-944a-28e8fb8f1814) is enabled for Bing, it can block chat providers for Copilot in Windows. The following network changes block the chat providers for Copilot in Windows and Edge:

   - Mapping `www.bing.com` to `strict.bing.com`
   - Mapping `edgeservices.bing.com` to `strict.bing.com`
   - Blocking `bing.com`

- If Copilot with commercial data protection is turned on for your organization, users can access it through Edge mobile when signed in with their work account. If you would like to remove the Bing Chat button from the Edge mobile interface, you can use an [Intune Mobile Application Management (MAM) policy for Microsoft Edge](/mem/intune/apps/manage-microsoft-edge) to remove it:

    | Key                                          | Value                                                                      |
    |:---------------------------------------------|:---------------------------------------------------------------------------|
    | com.microsoft.intune.mam.managedbrowser.Chat | **true** (default) shows the interface </br> **false** hides the interface |

### Microsoft Edge policies

- If [HubsSidebarEnabled](/deployedge/microsoft-edge-policies#hubssidebarenabled) is set to `disabled`, it blocks Copilot in Edge from being displayed.
- If [DiscoverPageContextEnabled](/deployedge/microsoft-edge-policies#discoverpagecontextenabled) is set to `disabled`, it blocks Copilot from reading the current webpage context. The chat providers need access to the current webpage context for providing page summarizations and sending user selected strings from the webpage into the chat provider.

### Search settings

- Setting [ConfigureSearchOnTaskbarMode](/windows/client-management/mdm/policy-csp-search#configuresearchontaskbarmode) to `Hide` might interfere with the Copilot in Windows user experience.
- Setting [AllowSearchHighlights](/windows/client-management/mdm/policy-csp-search#allowsearchhighlights) to `disabled` might interfere with the Copilot in Windows and the Copilot in Edge user experiences.

### Account settings

- The [AllowMicrosoftAccountConnection](/windows/client-management/mdm/policy-csp-accounts#allowmicrosoftaccountconnection) setting might allow users to use their personal Microsoft account with Copilot in Windows and Copilot in Edge.
- The [RestrictToEnterpriseDeviceAuthenticationOnly](/windows/client-management/mdm/policy-csp-accounts#restricttoenterprisedeviceauthenticationonly) setting might prevent access to chat providers since it blocks user authentication.

## Microsoft's commitment to responsible AI

Microsoft has been on a responsible AI journey since 2017, when we defined our principles and approach to ensuring this technology is used in a way that is driven by ethical principles that put people first. For more about our responsible AI journey, the ethical principles that guide us, and the tooling and capabilities we've created to assure that we develop AI technology responsibly, see [Responsible AI](https://www.microsoft.com/ai/responsible-ai).
