---
title: Sicurezza della replica su Internet | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], Internet
- Internet [SQL Server replication], security
ms.assetid: 25b7af05-2721-4b24-9083-fb671e8bf4e0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 78dfc544d7fd01f6641df6c0968d4a59a668cdd3
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54132521"
---
# <a name="securing-replication-over-the-internet"></a>Sicurezza della replica su Internet
  La replica su Internet garantisce una notevole flessibilità, in particolare ai Sottoscrittori mobili, tuttavia richiede una configurazione appropriata per assicurare un livello di sicurezza adeguato. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] consiglia di utilizzare una delle due tecniche seguenti per la condivisione protetta delle informazioni su Internet:  
  
-   Rete privata virtuale (VPN, Virtual Private Network)  
  
-   Opzione di sincronizzazione tramite il Web per la replica di tipo merge  
  
## <a name="virtual-private-network"></a>Rete privata virtuale  
 Le reti private virtuali costituiscono un approccio semplice e affidabile, strutturato su più livelli, alla replica dei dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] su Internet. Dal punto di vista logico, la connessione VPN su Internet opera analogamente a un collegamento su rete WAN tra siti.  
  
 A tale scopo è necessario consentire agli utenti l'esecuzione del tunneling su Internet o su un'altra rete pubblica utilizzando un protocollo disponibile in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows NT 4.0 o in [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 2000, ad esempio [!INCLUDE[msCoName](../../../includes/msconame-md.md)] PPTP (Point-to-Point Tunneling Protocol) oppure il protocollo L2TP (Layer Two Tunneling Protocol) disponibile nel sistema operativo Windows 2000. Questo processo consente di ottenere un livello di sicurezza e di caratteristiche simile a quello disponibile in una rete privata.  
  
 Per ulteriori informazioni sulla configurazione di una rete VPN, vedere la documentazione di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows.  
  
## <a name="web-synchronization-through-iis"></a>Sincronizzazione tramite il Web con IIS  
 L'opzione di sincronizzazione tramite il Web per la replica di tipo merge consente di replicare i dati utilizzando il protocollo HTTPS e costituisce, pertanto, un approccio conveniente alla replica dei dati attraverso un firewall. Per altre informazioni, vedere [Configurare la sincronizzazione Web](../configure-web-synchronization.md) and [Architettura di sicurezza per la sincronizzazione tramite il Web](security-architecture-for-web-synchronization.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Replication Security Best Practices](replication-security-best-practices.md)   
 [Sicurezza della replica di SQL Server](view-and-modify-replication-security-settings.md)  
  
  
