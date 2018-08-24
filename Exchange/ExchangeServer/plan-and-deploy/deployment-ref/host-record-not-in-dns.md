---
title: "The Host record for the local computer cannot be found in the DNS database [HostRecordMissing]"
ms.author: dstrome
author: dstrome
manager: serdars
ms.date: 12/20/2016
ms.audience: Developer
ms.topic: reference
f1_keywords:
- 'ms.exch.setupreadiness.HostRecordMissing'
ms.prod: exchange-server-it-pro
localization_priority: Normal
ms.assetid: 2f18cb65-29fe-4b72-8d68-52fd503d5673
description: ""
---

# The Host record for the local computer cannot be found in the DNS database [HostRecordMissing]

Microsoft Exchange Server 2016 Setup can't continue because the Host (A) record for this computer can't be found in the Domain Name System (DNS) database.
  
Exchange 2016 Setup requires that the local computer have a valid HOST (A) record registered with the authoritative DNS database for the domain.
  
Exchange depends on DNS Host (A) records for the IP Address of its next internal or external destination server.
  
To resolve this issue:
  
- Verify that the local TCP/IP configuration points to the correct DNS server. For more information, see [Configure TCP/IP settings](https://go.microsoft.com/fwlink/p/?linkid=108281).
    
- Use Nslookup.exe to verify that the Host (A) record exists on the DNS server. For more information, see [To verify A resource records exist in DNS](https://go.microsoft.com/fwlink/?LinkId=63001).
    
For information about DNS name resolution, troubleshooting, and Host (A) records, see the following:
  
- [Troubleshooting DNS](https://go.microsoft.com/fwlink/p/?LinkId=294828)
    
- [Managing resource records](https://go.microsoft.com/fwlink/p/?LinkId=294829)
    
Having problems? Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkId=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkId=267542), or [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkId=285351).
