---
title: Troubleshooting ActiveSync.Protocol Health Set
TOCTitle: Troubleshooting ActiveSync.Protocol Health Set
ms:assetid: 7351f881-08b2-4504-99f2-63e7acdfcc35
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.scom.activesync.protocol(v=EXCHG.150)
ms:contentKeyID: 49720823
ms.reviewer: 
ms.topic: article
description: How to troubleshoot the ActiveSync.Protocol health set in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Troubleshooting ActiveSync.Protocol Health Set

_**Applies to:** Exchange Server 2013_

The ActiveSync.Protocol health set monitors the overall health of the Exchange ActiveSync communications protocol on your Mailbox servers. If you receive an alert the ActiveSync.Protocol health set is unhealthy, the alert indicates an issue that may affect the ActiveSync components on the Mailbox server that's indicated in the alert.

## Explanation

The ActiveSync.Protocol health set works with the **ActiveSync** health set. For detailed information about the ActiveSync health set, see [Troubleshooting ActiveSync Health Set](troubleshooting-activesync-health-set.md).

## User Action

It's possible the ActiveSync service recovered after it issued the alert. So, when you receive an alert that the ActiveSync health set is unhealthy, first verify the issue still exists. See [Troubleshooting ActiveSync Health Set](troubleshooting-activesync-health-set.md).

## For More Information

[Exchange ActiveSync](../../exchange-activesync-exchange-2013-help.md)

[Mobile devices](../../mobile-devices-exchange-2013-help.md)

[Exchange ActiveSync virtual directory management tasks](../../exchange-activesync-virtual-directory-management-tasks-exchange-2013-help.md)
