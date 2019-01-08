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
ms.openlocfilehash: f0af2d4357c74d9ce7bec74e1b787ed259b04977
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52797359"
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
 [Sicurezza e protezione #40;replica&#41;](security-and-protection-replication.md)  
  
  
