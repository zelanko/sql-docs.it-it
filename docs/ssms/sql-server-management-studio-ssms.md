---
title: SQL Server Management Studio (SSMS)
description: Descrizione di SQL Server Management Studio (SSMS) e delle relative funzionalità.
ms.prod: sql
ms.technology: ssms
ms.topic: overview
author: markingmyname
ms.author: maghan
ms.reviewer: ''
f1_keywords:
- sql13.ssms.viewhelp.f1
helpviewer_keywords:
- SQL Server Management Studio
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.custom: ''
ms.date: 05/29/2019
ms.openlocfilehash: 3f80cc74cc20c2ed02e32577fadbe13a5bf7dd38
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66500344"
---
# <a name="what-is-sql-server-management-studio-ssms"></a>Che cos'è SQL Server Management Studio (SSMS)?

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) è un ambiente integrato per la gestione di qualsiasi infrastruttura SQL. Usare SSMS per l'accesso, la configurazione, la gestione, l'amministrazione e lo sviluppo di tutti i componenti di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], database SQL di Azure e Azure SQL Data Warehouse. SSMS è una singola utilità completa che integra un'ampia gamma di strumenti grafici con numerosi editor di script avanzati per offrire accesso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] per gli sviluppatori e gli amministratori di database qualsiasi sia il livello di competenza.

- [**Scaricare SQL Server Management Studio (SSMS)** ](download-sql-server-management-studio-ssms.md)
- [**Scaricare SQL Server Developer**](https://my.visualstudio.com/Downloads?q=SQL%20Server%20Developer)
- [**Scaricare Visual Studio**](https://www.visualstudio.com/downloads/)

## <a name="sql-server-management-studio-components"></a>Componenti di SQL Server Management Studio  
  
|Descrizione|Componente|  
|---------------|---------|  
|Usare **Esplora oggetti** per visualizzare e gestire tutti gli oggetti in una o più istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|[Esplora oggetti](../ssms/object/object-explorer.md)|  
|Come usare **Esplora modelli** per compilare e gestire file di testo preimpostato per velocizzare lo sviluppo di query e script.|[Esplora modelli](../ssms/template/template-explorer.md)|  
|Come usare la funzionalità **Esplora soluzioni** deprecata per compilare i progetti usati per gestire elementi di amministrazione quali script e query.|[Esplora soluzioni](../ssms/solution/solution-explorer.md)|  
|Come usare gli strumenti di progettazione visivi inclusi in [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].|[Visual Database Tools](../ssms/visual-db-tools/visual-database-tools.md)|  
|Come usare gli editor di linguaggio di [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per compilare ed eseguire il debug di query e script in modo interattivo.|[Editor di query e di testo (SQL Server Management Studio)](../relational-databases/scripting/query-and-text-editors-sql-server-management-studio.md)|

## <a name="sql-server-management-studio-for-business-intelligence"></a>SQL Server Management Studio per Business Intelligence

Per accedere, configurare, gestire e amministrare [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] e [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], utilizzare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Sebbene le tre tecnologie di Business Intelligence si basino tutte su [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], le attività amministrative associate a ciascuna di esse sono leggermente diverse.
  
> [!NOTE]
> Per creare e modificare soluzioni [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , utilizzare [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)]e non [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] è un ambiente di sviluppo basato su [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].
  
### <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Gestione di soluzioni Analysis Services tramite SQL Server Management Studio

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] consente di gestire oggetti di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] , ad esempio eseguendo backup ed elaborando oggetti.
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] include un progetto script di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] in cui è possibile sviluppare e salvare script creati in MDX (Multidimensional Expressions), DMX (Data Mining Extensions) e XMLA (XML per Analysis). Usare i progetti script di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] per eseguire attività di gestione o ricreare oggetti, ad esempio database e cubi in istanze di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] . È possibile, ad esempio, sviluppare uno script XMLA in un progetto script di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] per la creazione diretta di nuovi oggetti in un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] esistente. È possibile salvare i progetti script di [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] come parte di una soluzione e integrarli con il controllo del codice sorgente.
  
Per altre informazioni su come usare [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], vedere [Sviluppo e implementazione tramite SQL Server Management Studio](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).
  
### <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Gestione di soluzioni Integration Services tramite SQL Server Management Studio

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] consente di usare il servizio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] per gestire i pacchetti e monitorare i pacchetti in esecuzione. È inoltre possibile utilizzare [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] per organizzare pacchetti in cartelle, eseguire pacchetti, importare ed esportare pacchetti, eseguire la migrazione di pacchetti DTS (Data Transformation Services) e aggiornare pacchetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .

### <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Gestione di progetti di Reporting Services tramite SQL Server Management Studio

Utilizzare SQL Server Management Studio per abilitare le funzionalità di Reporting Services, amministrare il server e i database e gestire ruoli e processi.

Lo strumento consente di gestire pianificazioni condivise tramite la cartella Pianificazioni condivise e di gestire i database del server di report (ReportServer e ReportServerTempdb). È inoltre possibile creare un ruolo RSExecRole nel database di sistema Master quando si sposta un database del server di report in un'istanza nuova o diversa del Motore di database SQL Server ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]). Per ulteriori informazioni su queste attività, vedere gli argomenti seguenti:  

- [Procedure per SQL Server Management Studio](https://msdn.microsoft.com/60685458-9108-47bf-820a-5e7db454d408)
- [Amministrazione del database del server di report](../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)
- [Procedura: Creare RSExecRole](../reporting-services/security/create-the-rsexecrole.md)
  
Per gestire il server è inoltre possibile abilitare e configurare numerose funzionalità, configurare le impostazioni predefinite del server e gestire ruoli e processi. Per ulteriori informazioni su queste attività, vedere gli argomenti seguenti:

- [Procedura: Impostare le proprietà di un server di report (Management Studio)](https://msdn.microsoft.com/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)
- [Procedura: Creare, eliminare o modificare un ruolo (Management Studio)](https://msdn.microsoft.com/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)
- [Attivazione e disabilitazione della stampa sul lato client per Reporting Services](https://msdn.microsoft.com/0e709c96-7517-4547-8ef6-5632f8118524)

## <a name="non-english-language-versions-of-sql-server-management-studio-ssms"></a>Versioni in lingua non inglese di SQL Server Management Studio (SSMS)

Il blocco per l'installazione in lingue miste è stato rimosso. È possibile installare SSMS in tedesco in una versione di Windows in francese. Se la lingua del sistema operativo non corrisponde a quella di SSMS, l'utente deve cambiare la lingua in Strumenti > Opzioni > Impostazioni internazionali, altrimenti SSMS visualizzerà l'interfaccia utente in inglese.

Per altre informazioni sulle diverse impostazioni locali con le versioni precedenti, fare riferimento a [Installare versioni in lingua non inglese di SQL Server Management Studio (SSMS)](install-other-languages.md).

## <a name="support-policy-for-ssms"></a>Criteri di supporto per SSMS

- A partire da SSMS 17.0, il team degli strumenti di SQL ha adottato i [criteri moderni relativi al ciclo di vita Microsoft](https://support.microsoft.com/help/30881/modern-lifecycle-policy).
- Vedere l'[annuncio dei criteri relativi al ciclo di vita moderni](https://support.microsoft.com/help/447912/announcing-microsoft-modern-lifecycle-policy) originale.
- Per altre informazioni, vedere [Domande frequenti sui criteri moderni relativi al ciclo di vita](https://support.microsoft.com/help/30882/modern-lifecycle-policy-faq).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

## <a name="next-steps"></a>Passaggi successivi

- [Installare versioni in lingua non inglese di SQL Server Management Studio (SSMS)](install-other-languages.md)
- [Esercitazione: SQL Server Management Studio](tutorials/tutorial-sql-server-management-studio.md)
- [Esercitazione: Scrittura di istruzioni Transact-SQL](https://msdn.microsoft.com/2addc9be-67d0-423d-a457-192fe9d7d058)
- [Sviluppo e implementazione tramite SQL Server Management Studio](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)
- [Reporting Services in SQL Server Data Tools](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)
- [Esercitazione: SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/tutorials/tutorial-sql-server-management-studio)

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]