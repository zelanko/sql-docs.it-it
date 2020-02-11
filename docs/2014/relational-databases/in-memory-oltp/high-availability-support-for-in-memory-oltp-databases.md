---
title: Supporto della disponibilità elevata per i database OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 2113a916-3b1e-496c-8650-7f495e492510
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 37c719beb625a533c2d8f279a8500365c4786c05
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62990577"
---
# <a name="high-availability-support-for-in-memory-oltp-databases"></a>Supporto della disponibilità elevata per i database OLTP in memoria
  I database che contengono tabelle ottimizzate per la memoria, con o senza stored procedure compilate native, sono completamente supportati con i gruppi di disponibilità AlwaysOn.  Non c'è alcuna differenza di configurazione e supporto per i database contenenti oggetti [!INCLUDE[hek_2](../../includes/hek-2-md.md)] rispetto a quelli che non li contengono.  
  
## <a name="alwayson-availability-groups-and-in-memory-oltp-databases"></a>Gruppi di disponibilità AlwaysOn e database OLTP in memoria  
 La configurazione dei database con componenti [!INCLUDE[hek_2](../../includes/hek-2-md.md)] offre quanto segue:  
  
-   **Un'esperienza completamente integrata**   
    È possibile configurare i database contenenti tabelle ottimizzate per la memoria usando la stessa procedura guidata con lo stesso livello di supporto sia per le repliche secondarie asincrone sia per quelle sincrone. Inoltre, il monitoraggio dello stato viene fornito mediante il noto dashboard AlwaysOn in SQL Server Management Studio.  
  
-   **Tempo di failover paragonabile**   
    Le repliche secondarie mantengono lo stato in memoria delle tabelle durevoli ottimizzate per la memoria. In caso di failover automatico o forzato, il tempo di failover al nuovo database primario è paragonabile a quello del failover a tabelle basate su disco, in quanto non è necessario il ripristino. Le tabelle con ottimizzazione per la memoria create come SCHEMA_ONLY sono supportate in questa configurazione. Tuttavia, le modifiche a queste tabelle non vengono registrate e pertanto non saranno presenti dati in queste tabelle nella replica secondaria.  
  
-   **Secondario leggibile**   
    È possibile accedere ed eseguire query su tabelle ottimizzate per la memoria nella replica secondaria se questa è stata configurata per l'accesso in lettura. Per altre informazioni, vedere [Repliche secondarie attive: Repliche secondarie leggibili &#40;Gruppi di disponibilità AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
## <a name="failover-clustering-instance-fci-and-in-memory-oltp-databases"></a>Istanza di clustering di failover e database OLTP in memoria  
 Per ottenere disponibilità elevata in una configurazione di archiviazione condivisa, è possibile impostare il clustering di failover nelle istanze con uno o più database con tabelle ottimizzate per la memoria. Per l'impostazione di un'istanza di clustering di failover, è necessario considerare i fattori seguenti.  
  
-   **Obiettivo del tempo di ripristino**   
    Il tempo di failover sarà probabilmente maggiore perché le tabelle ottimizzate per la memoria devono essere caricate in memoria prima che il database venga reso disponibile.  
  
-   **Tabelle SCHEMA_ONLY**   
    Tenere presente che le tabelle SCHEMA_ONLY saranno vuote e senza righe dopo il failover. Si tratta di un comportamento previsto definito dall'applicazione. Questo comportamento corrisponde esattamente a ciò che succede quando si riavvia un database [!INCLUDE[hek_2](../../includes/hek-2-md.md)] con una o più tabelle SCHEMA_ONLY.  
  
## <a name="support-for-transaction-replication-in-in-memory-oltp"></a>Supporto per la replica transazionale in OLTP In memoria  
 Le tabelle con funzione di sottoscrittori di replica transazionale, esclusa la replica transazionale peer-to-peer, possono essere configurate come tabelle ottimizzate per la memoria. Le altre configurazioni di replica non sono compatibili con le tabelle ottimizzate per la memoria.  Per altre informazioni, vedere [replica in Sottoscrittori di tabelle con ottimizzazione](../replication/replication-to-memory-optimized-table-subscribers.md)per la memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [Gruppi di disponibilità AlwaysOn (SQL Server)](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)   
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Repliche secondarie attive: repliche secondarie leggibili &#40;Gruppi di disponibilità AlwaysOn&#41;](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Replica in sottoscrittori di tabelle con ottimizzazione per la memoria](../replication/replication-to-memory-optimized-table-subscribers.md)  
  
  
