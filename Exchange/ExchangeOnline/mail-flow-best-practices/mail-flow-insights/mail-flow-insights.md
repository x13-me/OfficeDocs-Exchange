---
title: "Mail flow insights in the modern Exchange admin center"
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
manager: dansimp
audience: ITPro
ms.topic: article
ms.service: exchange-online
localization_priority: Normal
ms.assetid:
description: Admins can learn about the mail flow dashboard in the modern Exchange admin center, including insights, reports, and widgets.
ms.custom:
---

# Mail flow reports and insights in the modern Exchange admin center

Admins can use mail flow reports and the insights dashboard in the modern Exchange admin center (modern EAC) to discover trends and take action to fix issues related to mail flow in their organization.

## Mail flow reports

The following mail flow reports are available:

- [Auto forwarded messages report](mfi-auto-forwarded-messages-report.md)

- [Email issues for priority accounts report](mfi-email-issues-for-priority-accounts.md)

- [Inbound messages report](mfi-inbound-messages-report.md)

- Non-accepted domain report

- Non-delivery details report

- Outbound messages report

- Queued messages report

- SMTP AUTH clients report

- Top domain mailflow status report

To see the mail flow reports, open the modern EAC at <https://admin.exchange.microsoft.com/#/>, expand **Reports**, and then select **Mail flow**.

To go directly to the mail flow reports, open <https://admin.exchange.microsoft.com/#/reports/vipmailflowdetails>.

## Mail flow insights

The following mail flow insights are available:

- Fix possible mail loop

- Fix slow mail flow rules

- New domains being forwarded email

- New users forwarding email

To see the mail flow insights, open the modern EAC at <https://admin.exchange.microsoft.com/#/> and select **Insights**.

To go directly to the mail flow insights dashboard, open <https://admin.exchange.microsoft.com/#/insights>.

## Required permissions

To view and use the mail flow reports, you need to be a member of one of the following role groups in Exchange Online:

- Organization Management
- Security Administrator<sup\>*</sup>
- Security Reader<sup>\*</sup>
- View-only Organization Management
- View-Only Recipients

To use the mail flow insights to take corrective action, you need to be a member of one of the following role groups:

- Organization Management
- Security Administrator<sup\>*</sup>

For read only access to the mail flow insights, you need to be a member of one of the following role groups:

- Security Reader<sup>\*</sup>
- View-only Organization Management
- View-Only Recipients

For more information, see [Permissions in Exchange Online](../../permissions-exo/permissions-exo.md) and [Manage role groups in Exchange Online](../../permissions-exo/role-groups.md).

<sup\>*</sup> You control membership in these role groups in the [Azure Active Directory admin center](https://aad.portal.azure.com).
