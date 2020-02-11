---
title: Archivio BLOB remoti (RBS) e Gruppi di disponibilità AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 01a70258-d4fd-40bc-bc44-c490b5d6c420
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 32b2ab48c3406c9820ca264a1cef236a041a5924
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62814552"
---
# <a name="remote-blob-store-rbs-and-alwayson-availability-groups-sql-server"></a>Archivio BLOB remoti (RBS) e gruppi di disponibilità AlwaysOn (SQL Server)
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]può offrire una soluzione di disponibilità elevata e ripristino di emergenza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]per gli oggetti BLOB (BLOB) di [archiviazione BLOB remoti](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md) . 
  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] protegge tutti i metadati e gli schemi di RBS archiviati in un database di disponibilità replicandoli nelle repliche secondarie. Questo è il database del contenuto di SharePoint. In generale, tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] questi metadati di RBS vengono archiviati in modo indipendente dal BLOB.  
  
 La protezione dei dati BLOB di RBS dipende dal percorso dell'archivio BLOB, come riportato di seguito:  
  
|Percorso dell'archivio BLOB|Possibilità di protezione dei dati BLOB tramite i gruppi di disponibilità|  
|-------------------------|-----------------------------------------------------|  
|Stesso database in cui sono contenuti i metadati di RBS (archiviato utilizzando un provider FILESTREAM remoto di RBS)|Sì|  
|Database diverso nella stessa istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (archiviato utilizzando un provider FILESTREAM remoto di RBS)|Sì<br /><br /> È consigliabile inserire questo database nello stesso gruppo di disponibilità del database in cui sono contenuti i metadati di RBS.|  
|Database diverso in un'istanza differente di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (archiviato utilizzando un provider FILESTREAM remoto di RBS)|Sì<br /><br /> Questo database deve trovarsi in un gruppo di disponibilità separato.|  
|Archivio BLOB di terze parti|No<br /><br /> Per proteggere questi dati BLOB, utilizzare i meccanismi di disponibilità elevata del provider dell'archivio BLOB.|  
  
##  <a name="Limitations"></a>Limitazioni  
  
-   I gestori RBS devono essere indirizzati alla replica primaria.  
  
##  <a name="Recommendations"></a> Raccomandazioni  
  
-   Utilizzare un listener del gruppo di disponibilità. Per altre informazioni, vedere [Listener del gruppo di disponibilità, connettività client e failover dell'applicazione &#40;SQL Server&#41;](../../listeners-client-connectivity-application-failover.md).  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Gestione di archivio BLOB remoto](https://msdn.microsoft.com/library/gg316773\(SQL.105\).aspx) ( [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] nella documentazione online di)  
  
-   [Esecuzione](https://blogs.msdn.com/b/sqlrbs/archive/2010/03/19/running-rbs-maintainer.aspx) di gestione RBS (Blog)  
  
-   [Configurare archiviazione BLOB remoti (RBS) con il provider FILESTREAM (SharePoint 2010)](https://blogs.msdn.com/b/mvpawardprogram/archive/2012/04/02/configure-remote-blob-storage-rbs-with-the-filestream-provider-sharepoint-2010.aspx) (Blog)  
  
## <a name="see-also"></a>Vedere anche  
 [Connettività client AlwaysOn &#40;SQL Server&#41;](always-on-client-connectivity-sql-server.md)   
 [Archivio Blob remoto &#40;RBS&#41; &#40;SQL Server&#41;](../../../relational-databases/blob/remote-blob-store-rbs-sql-server.md)  
  
  
