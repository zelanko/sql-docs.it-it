---
title: Aggiornare Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- upgrading databases
- databases [Analysis Services], upgrading
- installing Analysis Services, side-by-side installations
- Analysis Services upgrades
- Analysis Services upgrades, about upgrading Analysis Services
- SSAS, database migration
- upgrading Analysis Services
- installing Analysis Services, upgrading
- SSAS, upgrading
ms.assetid: a131d329-386e-4470-aaa9-ffcde4e5ec0c
author: Minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8bbec3cd552434070d76913f72812b302440bcdb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62775031"
---
# <a name="upgrade-analysis-services"></a>Aggiornare Analysis Services
  Utilizzare il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per informazioni dettagliate sull'aggiornamento [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in modalità SharePoint, vedere [aggiornare PowerPivot per SharePoint](upgrade-power-pivot-for-sharepoint.md). Per altre informazioni sull'aggiornamento di un Server SQL esistente dell'istanza, vedere [esegue l'aggiornamento a SQL Server 2014 usando l'installazione guidata di &#40;installazione&#41;](upgrade-sql-server-using-the-installation-wizard-setup.md).  
  
## <a name="known-upgrade-issues"></a>Problemi di aggiornamento noti  
 Prima di effettuare l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere gli argomenti seguenti:  
  
-   [Note sulla versione di SQL Server 2014](https://go.microsoft.com/fwlink/?LinkID=296445).  
  
-   Per informazioni sulle [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] caratteristiche e funzionalità sono stati non più disponibile, deprecate o modificate vedere [Analysis Services Backward Compatibility](../../analysis-services/analysis-services-backward-compatibility.md).  
  
## <a name="pre-upgrade-checklist"></a>Elenco di controllo preliminare all'aggiornamento  
 Prima di eseguire l'aggiornamento, vedere le informazioni seguenti:  
  
-   [Aggiornamenti di versione ed edizione supportati](supported-version-and-edition-upgrades.md)  
  
-   [Requisiti hardware e software per l'installazione di SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
-   [Parametri di controllo di Controllo configurazione sistema](check-parameters-for-the-system-configuration-checker.md)  
  
-   [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
-   [Backup e ripristino di database di Analysis Services](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
-   [Usare la Preparazione aggiornamento per preparare gli aggiornamenti](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
## <a name="upgrading-analysis-services"></a>Aggiornamento di Analysis Services  
 È possibile scegliere diversi approcci per aggiornare il server e i dati:  
  
-   Un' **aggiornamena sul posa** sostituisce i file di programma esistenti con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] i file di programma. I database rimangono nello stesso percorso. Le cartelle del programma vengono aggiornate in modo da riflettere il nuovo nome.  
  
-   Oggetto **aggiornamento side-by-side** è una nuova installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] nello stesso computer che dispone di un'istanza di Analysis Services esistente. È possibile spostare database nella nuova istanza dello stesso computer, quindi disinstallare la versione precedente se non viene più utilizzata.  
  
-   È possibile inoltre installare Analysis Services in un nuovo hardware e, successivamente, eseguire la migrazione dei database esistenti in tale server.  
  
## <a name="in-place-upgrade"></a>Aggiornamento sul posto  
 È possibile aggiornare un'istanza esistente di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e, come parte del processo di aggiornamento, eseguire automaticamente la migrazione dei database esistenti dall'istanza precedente a quella nuova. Poiché i metadati e i dati binari sono compatibili tra le due versioni, i dati verranno mantenuti in seguito all'aggiornamento e non sarà necessario eseguirne la migrazione manuale.  
  
 Per aggiornare un'istanza esistente, eseguire il programma di installazione e specificare il nome dell'istanza esistente come nome della nuova istanza.  
  
## <a name="upgrading-databases"></a>Aggiornamento di database  
 I database creati in versioni precedenti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] vengono eseguiti nel server aggiornato con un'impostazione del livello di compatibilità di database precedente. I database creati nelle versioni seguenti dispongono di un livello di compatibilità del database pari a 105. È possibile modificare il livello di compatibilità se si desidera utilizzare funzionalità che richiedono un livello di compatibilità del database più recente. In caso contrario, i database possono essere eseguiti nel server aggiornato utilizzando le impostazioni originali. Per altre informazioni, vedere [impostare il livello di compatibilità di un Database multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md).  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità supportate dalle edizioni di SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Pianificazione di un'installazione di SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Informazioni sull'architettura Microsoft OLAP](../../analysis-services/multidimensional-models/olap-physical/understanding-microsoft-olap-architecture.md)   
 [Aggiornare PowerPivot per SharePoint](upgrade-power-pivot-for-sharepoint.md)   
 [Installazione di Analysis Services in modalità Multidimensionale e Data Mining](../../sql-server/install/install-analysis-services-in-multidimensional-and-data-mining-mode.md)   
 [Installazione di PowerPivot per SharePoint 2010](../../sql-server/install/powerpivot-for-sharepoint-2010-installation.md)  
  
  
