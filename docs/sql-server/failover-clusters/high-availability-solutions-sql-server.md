---
title: Soluzioni a disponibilità elevata (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 05/19/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- high availability [SQL Server], solutions
- Database Engine [SQL Server], availability
- database availability [SQL Server]
- availability [SQL Server]
- server availability [SQL Server]
ms.assetid: b2eda634-0f8e-4703-801b-7ba895544ff5
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f5c07a9689453e11058dedcdcd0d014f01b6e480
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52502417"
---
# <a name="high-availability-solutions-sql-server"></a>Soluzioni a disponibilità elevata (SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento vengono presentate alcune soluzioni a disponibilità elevata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che consentono di migliorare la disponibilità di server o database. Una soluzione a disponibilità elevata maschera gli effetti di un malfunzionamento hardware o software e mantiene la disponibilità delle applicazioni in modo che il tempo di inattività percepito dagli utenti sia ridotto al minimo.    
    
   
>  **Nota.** Per conoscere le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che supportano una determinata soluzione a disponibilità elevata, vedere la sezione relativa alla disponibilità elevata (Always On) di [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
     
    
##  <a name="TermsAndDefinitions"></a> Panoramica delle soluzioni a disponibilità elevata di SQL Server    
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono disponibili diverse opzioni per creare la disponibilità elevata per un server o un database. Le opzioni di disponibilità elevata sono riportate di seguito:    
    
*  Istanze del cluster di failover Always On    
 Nell'offerta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Always On le istanze del cluster di failover Always On usano la funzionalità clustering di failover di Windows Server (WSFC, Windows Server Failover Clustering) per fornire la disponibilità elevata in locale tramite la ridondanza a livello di istanza del server, ovvero un'*istanza del cluster di failover*. Un'istanza del cluster di failover è una sola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installata nei nodi del clustering di failover di Windows Server (WSFC) e, possibilmente, in più subnet. In rete, un'istanza del cluster di failover appare come un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in un singolo computer, le cui funzionalità forniscono il failover da un nodo WSFC a un altro, quando il nodo corrente non è più disponibile.    
    
 Per altre informazioni, vedere [Istanze del cluster di failover Always On &#40;SQL Server&#41;](../../sql-server/failover-clusters/windows/always-on-failover-cluster-instances-sql-server.md).    
    
*  [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]    
 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] è una soluzione di ripristino di emergenza a disponibilità elevata a livello aziendale introdotta in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] per ottimizzare la disponibilità per uno o più database. [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] richiede che le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] risiedano sui nodi WSFC (Windows Server Failover Clustering). Per altre informazioni, vedere [Gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md).    
    
  
>  **Nota.** Un'istanza del cluster di failover può sfruttare [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] per fornire il ripristino di emergenza remoto a livello di database. Per altre informazioni, vedere [Clustering di failover e gruppi di disponibilità Always On &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md).    
    
*  Mirroring del database. **Nota.** [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] È consigliabile utilizzare [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] in alternativa.     
Il mirroring del database è una soluzione per aumentare la disponibilità del database supportando un failover quasi istantaneo. Il mirroring del database è utilizzabile per gestire un singolo database di standby, oppure un *database mirror*, per un database di produzione corrispondente detto *database principale*. Per altre informazioni, vedere [Mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md).    
    
*  Log shipping    
 Analogamente al mirroring del database e a [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] , il log shipping opera a livello del database. È possibile usare il log shipping per gestire uno o più database in modalità warm standby (definiti *database secondari*) per un singolo database di produzione definito *database primario*. Per altre informazioni sul log shipping, vedere [Informazioni sul log shipping &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).    
    
##  <a name="RecommendedSolutions"></a> Soluzioni consigliate per l'utilizzo di SQL Server per proteggere i dati    
 Indicazione per la protezione dei dati per l'ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :    
    
-   Per la protezione dei dati con una soluzione disco condivisa di terze parti (SAN), è consigliabile usare le istanze del cluster di failover Always On.    
    
-   Per protezione dei dati tramite [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si consiglia di usare [!INCLUDE[ssHADR](../../includes/sshadr-md.md)].    
    
       >  È consigliabile usare il log shipping se si esegue una versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che non supporta [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]. Per informazioni sulle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssHADR](../../includes/sshadr-md.md)]vedere la sezione relativa alla disponibilità elevata (Always On) di [Funzionalità supportate dalle edizioni di SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).    
    
## <a name="see-also"></a>Vedere anche    
 [WSFC &#40;Windows Server Failover Clustering&#41; con SQL Server](../../sql-server/failover-clusters/windows/windows-server-failover-clustering-wsfc-with-sql-server.md)     
 [Mirroring del database: Interoperabilità e coesistenza &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-interoperability-and-coexistence-sql-server.md)     
 [Funzionalità del Motore di database deprecate in SQL Server 2016](../../database-engine/deprecated-database-engine-features-in-sql-server-2016.md)    
    
  

