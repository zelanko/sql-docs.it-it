---
title: Funzionalità di Master Data Services deprecate in SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 0d861d390989798ed9f33834cf42d6dcb8179ebe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971571"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>Funzionalità deprecate di Master Data Services in SQL Server 2014
  In questo argomento verranno descritte le funzionalità deprecate di [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] ancora disponibili in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Tali funzionalità verranno rimosse a partire da una delle prossime versioni di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. È consigliabile non usare le funzionalità deprecate nelle nuove applicazioni.  
  
## <a name="staging-process"></a>Processo di gestione temporanea  
 Il processo di gestione temporanea utilizzato in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] non è più disponibile nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] ; tuttavia è ancora disponibile in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Gli errori di gestione temporanea dal processo di gestione temporanea [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] non sono più visualizzati nell'interfaccia utente. I codici di errore popolati durante il processo di gestione temporanea sono ancora disponibili nelle tabelle di staging ed è possibile trovarli qui: [https://msdn.microsoft.com/library/ff487022.aspx](https://msdn.microsoft.com/library/ff487022.aspx) .  
  
 Le tabelle di staging (tblStgMember, tblStgMemberAttribute e tblStgRelationship) ancora sono disponibili nel database. La stored procedure utilizzata per iniziare il processo di gestione temporanea (mdm.udpStagingSweep) è ancora disponibile nel database.  
  
 Sono ancora disponibili i metodi del servizio Web che richiamano il processo di gestione temporanea.  
  
 Il set dell'intervallo di gestione temporanea in [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] si applica al processo di gestione temporanea in [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] e in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 Un nuovo, più elevato processo di gestione temporanea delle prestazioni è stato implementato in [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Importazione dati &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
## <a name="metadata"></a>Metadati  
 Sebbene il modello di metadati è ancora visualizzato nell'applicazione Web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] , non deve essere utilizzato. Verrà rimosso in una versione futura. Gli Utenti possono visualizzare anche più metadati nell'area funzionale **Esplora** ed è possibile creare più versioni del modello di metadati.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di Master Data Services non più supportate in SQL Server 2014](discontinued-master-data-services-features.md)  
  
  
