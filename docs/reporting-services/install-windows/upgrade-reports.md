---
description: Aggiornare i report (SSRS)
title: Aggiornare i report | Microsoft Docs
ms.date: 06/04/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], upgrading
- published reports [Reporting Services], upgrades
- custom report items, upgrading
- Reporting Services, upgrades
- upgrading Reporting Services
- snapshots [Reporting Services], upgrading
- report definition files [Reporting Services]
- .rdl files
ms.assetid: a1a10c67-7462-4562-9b07-a8822188a161
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1454c579739c892cc3d0c03211283589ba3e6b82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446026"
---
# <a name="upgrade-reports-ssrs"></a>Aggiornare i report (SSRS)

[!INCLUDE[ssrs-appliesto-sql2016-preview](../../includes/ssrs-appliesto-sql2016-preview.md)]

I file di definizione del report (con estensione rdl) esistenti vengono aggiornati automaticamente nei modi seguenti:  
  
-   Quando si apre un report impaginato in Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], la definizione del report viene aggiornata allo schema RDL attualmente supportato. Quando si specifica un server di report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] nelle proprietà del progetto, la definizione del report viene salvata in uno schema compatibile con il server di destinazione.  
  
-   Quando si aggiorna un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a un'installazione di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , i report e gli snapshot esistenti pubblicati in un server di report vengono compilati e aggiornati automaticamente al nuovo schema al momento della prima elaborazione. Se non può essere aggiornato automaticamente, il report viene elaborato utilizzando la modalità di compatibilità con le versioni precedenti. La definizione del report rimane nello schema originale.  
  
 Dopo l'aggiornamento di un report localmente o nel server di report, è possibile riscontrare errori, avvisi e messaggi aggiuntivi. Le modifiche apportate internamente al modello a oggetti e ai componenti di elaborazione interni dei report determinano infatti la visualizzazione di messaggi in caso di rilevamento di problemi sottostanti nel report. Per altre informazioni, vedere [Reporting Services Backward Compatibility](../../reporting-services/reporting-services-backward-compatibility.md).  
  
 Per altre informazioni sulle nuove funzionalità per [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], vedere [Novità di SQL Server Reporting Services (SSRS)](../what-s-new-in-sql-server-reporting-services-ssrs.md).  

##  <a name="versions-supported-by-upgrade"></a><a name="bkmk_versionsupported"></a> Versioni supportate per l'aggiornamento  
 I report creati in qualsiasi versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono essere aggiornati. Sono incluse le versioni seguenti:  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
##  <a name="report-definition-rdl-files-and-report-designer"></a><a name="bkmk_rdlfiles"></a> File di definizione del report (con estensione rdl) e Progettazione report  
 Un file di definizione del report include un riferimento allo spazio dei nomi RDL che specifica la versione dello schema di definizione del report utilizzata per convalidare il file con estensione rdl.  
  
 Quando si apre un file con estensione rdl in Progettazione report di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], se il report è stato creato per uno spazio dei nomi precedente, viene creato automaticamente un file di backup e aggiornato il report allo spazio dei nomi corrente. Questo è l'unico modo in cui è possibile aggiornare un file di definizione del report.  
  
 Le proprietà di distribuzione impostate possono modificare lo schema in cui è salvato il file di definizione del report. Per altre informazioni, vedere [Distribuzione e supporto della versione in SQL Server Data Tools &#40;SSRS&#41;](../../reporting-services/tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
 È possibile caricare un file con estensione rdl creato in una versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nella nuova versione e al primo uso verrà aggiornato automaticamente. Nel server di report il file di definizione del report viene archiviato nel formato originale. Il report viene aggiornato automaticamente la prima volta che viene visualizzato, ma il file di definizione del report archiviato rimane invariato.  
  
 Per identificare lo schema RDL corrente relativo a un report per un server di report o per Progettazione report, vedere [Individuare la versione dello schema di definizione del report &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
##  <a name="published-reports-and-report-snapshots"></a><a name="bkmk_publishedreports_and_snapshots"></a> Report pubblicati e snapshot dei report  
 Al primo utilizzo, il server di report tenta di aggiornare i report pubblicati e gli snapshot del report esistenti al nuovo schema di definizione del report, senza richiedere alcun intervento da parte dell'utente. Quando un report o uno snapshot del report viene visualizzato da un utente o quando il server di report elabora una sottoscrizione, viene eseguito il tentativo di aggiornamento. La definizione del report non viene sostituita, ma continua a essere archiviata nel server di report nello schema originale. Se non può essere aggiornato, il report viene eseguito in modalità di compatibilità con le versioni precedenti.  
  
##  <a name="backward-compatibility-mode"></a><a name="bkmk_backcompat"></a> Modalità di compatibilità con le versioni precedenti  
 Un report aggiornato in modo corretto viene elaborato dal componente Elaborazione report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Se non può essere aggiornato, il report viene elaborato dal componente Elaborazione report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità di compatibilità con le versioni precedenti. Un report non può essere elaborato da entrambi i componenti di elaborazione. Al primo utilizzo, un report viene aggiornato correttamente o viene contrassegnato per la compatibilità con le versioni precedenti.  
  
 Solo il componente Elaborazione report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] supporta le nuove funzionalità. Se un report non può essere aggiornato, è comunque possibile visualizzarlo, ma le nuove funzionalità non sono disponibili. Per utilizzare le nuove funzionalità, è necessario che un report sia aggiornato correttamente.  
  
##  <a name="upgrading-a-report-with-subreports"></a><a name="bkmk_subreports"></a> Aggiornamento di un report con sottoreport  
 Se in un report sono contenuti sottoreport, durante l'aggiornamento può verificarsi una delle quattro situazioni seguenti:  
  
-   Il report principale e tutti i sottoreport possono essere aggiornati correttamente e vengono quindi elaborati dal componente Elaborazione report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
-   Il report principale e tutti i sottoreport non possono essere aggiornati e vengono elaborati dal componente Elaborazione report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
-   Il report principale può essere aggiornato, ma uno o più sottoreport non possono essere aggiornati. In questo caso il report principale viene elaborato dal componente Elaborazione report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , mentre per il report visualizzabile viene generato un messaggio che indica l'impossibilità di elaborare il sottoreport nella posizione destinata al sottoreport che non è stato possibile aggiornare.  
  
-   Il report principale non può essere aggiornato, mentre uno o più sottoreport possono essere aggiornati. Il report principale viene elaborato dal componente Elaborazione report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] , mentre per il report visualizzabile viene generato un messaggio che indica l'impossibilità di elaborare il sottoreport nella posizione destinata al sottoreport.  
  
 Se viene visualizzato l'errore che indica l'impossibilità di elaborare il sottoreport, è necessario modificare la definizione del report principale o del sottoreport in modo che i report possano essere elaborati dalla stessa versione di Elaborazione report.  
  
 Ai report drill-through non viene applicata questa limitazione poiché vengono elaborati come report indipendenti.  
  
##  <a name="upgrading-a-report-with-custom-report-items"></a><a name="bkmk_CRIs"></a> Aggiornamento di un report con elementi del report personalizzati  
 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]I report di [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono contenere elementi del report personalizzati resi disponibili da fornitori di software di terze parti e installati dall'amministratore di sistema nel computer di creazione dei report e nel server di report. I report che contengono elementi del report personalizzati possono essere aggiornati nei modi seguenti:  
  
-   Un server di report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene aggiornato a un server di report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. I report pubblicati nel server di report vengono aggiornati automaticamente al primo utilizzo.  
  
-   Un report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene caricato in un server di report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]. Il report viene aggiornato automaticamente al primo utilizzo.  
  
-   Un report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene aperto in Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Viene creata una copia di backup del report originale e si verifica uno dei due casi seguenti:  
  
    1.  In tutti gli elementi del report personalizzati non sono presenti funzionalità non supportate. Gli elementi del report personalizzati vengono convertiti in elementi del report nel nuovo schema di definizione del report determinando l'aggiornamento dell'intero report. Se si salva il file, il salvataggio viene eseguito nello spazio dei nomi RDL corrente.  
  
    2.  In uno o più elementi del report personalizzati sono presenti funzionalità non supportate. In una finestra di dialogo viene richiesto all'utente se convertire gli elementi del report personalizzati o se lasciarli invariati.  
  
     Per ulteriori informazioni, vedere [Apertura di un report con elementi del report personalizzati in Progettazione report](#OpeningaReport) più avanti in questo argomento.  
  
 Per informazioni su come identificare lo spazio dei nomi RDL corrente per un server di report, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o un report, vedere [Individuare la versione dello schema di definizione del report &#40;SSRS&#41;](../../reporting-services/reports/find-the-report-definition-schema-version-ssrs.md).  
  
### <a name="upgrading-reports-on-a-report-server"></a>Aggiornamento di report in un server di report  
 La prima volta che un report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene eseguito in un server di report aggiornato a un server di report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], viene aggiornato automaticamente allo spazio dei nomi della definizione del report corrente supportato dal server di report. È possibile che il report fosse presente nel server di report prima dell'aggiornamento, fosse stato caricato con il portale Web o fosse stato pubblicato nel server di report da Progettazione report in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
 Nella tabella seguente viene elencata l'azione di aggiornamento eseguita dal server di report per tipi specifici di elementi del report personalizzati in un report.  
  
|Tipo di elemento del report personalizzato|Azione di aggiornamento eseguita nel server di report|  
|--------------|----------------------------------|  
|Elementi del report personalizzati di terze parti|Aggiornamento non eseguito.<br /><br /> Elaborazione eseguita dal componente Elaborazione report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|  
  
###  <a name="opening-a-report-with-cris-in-report-designer"></a><a name="OpeningaReport"></a> Apertura di un report con elementi del report personalizzati in Progettazione report  
 Se si apre un report di [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] con elementi del report personalizzati in Progettazione report in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], questo report viene aggiornato al nuovo schema di definizione del report. In base agli elementi del report personalizzati contenuti nel report, verrà effettuata una delle azioni seguenti:  
  
-   Vengono rilevati elementi del report personalizzati di terze parti. Se la versione di tali elementi installata nel computer di creazione del report non è compatibile con il nuovo schema RDL, nell'area di progettazione viene visualizzata una casella di testo con una lettera X rossa. È necessario contattare l'amministratore di sistema per installare nuove versioni degli elementi del report personalizzati di fornitori di terze parti compatibili con il nuovo schema RDL.  
  
 Il salvataggio di un report dopo che il report è stato aggiornato nell'ambiente di creazione rappresenta l'unico modo per aggiornare un report esistente al nuovo schema di definizione del report.  
  
###  <a name="convert-cri-dialog-box"></a><a name="bkmk_convertCRIdialog"></a> Finestra di dialogo per la conversione dell'elemento del report personalizzato  
 In questo report sono contenuti elementi del report personalizzati con funzionalità non supportate. Gli elementi del report personalizzati sono estensioni del linguaggio RDL (Report Definition Language) che supportano gli oggetti personalizzati che consentono di visualizzare i dati in un report e contengono componenti della fase di progettazione e della fase di esecuzione resi disponibili dai fornitori di software di terze parti.  
  
> [!NOTE]  
>  La scelta di supportare elementi del report personalizzati in un server di report è una decisione che spetta all'amministratore del sistema. Per visualizzare questi elementi, è necessario che i relativi componenti siano installati nel client di creazione dei report, in modo da poter visualizzare in anteprima un report, e nel server di report per visualizzare un report pubblicato o caricato. Per altre informazioni, vedere [Elementi dei report personalizzati](../../reporting-services/custom-report-items/custom-report-items.md) e la documentazione del fornitore di software di terze parti.  
  
 Alcuni elementi del report personalizzati possono essere convertiti in elementi del report con il nuovo formato di definizione. Utilizzare l'elenco seguente per decidere se convertire gli elementi del report personalizzati in questo report:  
  
-   **Sì** Scegliere **Sì** per convertire tutti gli elementi del report personalizzati nel report, laddove possibile. Le funzionalità non supportate negli elementi del report personalizzati non possono essere aggiornate e vengono rimosse dal file di definizione del report. Durante la visualizzazione del report è possibile notare le differenze nella visualizzazione degli elementi del report personalizzati.  
  
-   **No** Scegliere **No** se non si desidera convertire gli elementi del report personalizzati nel report. Gli elementi non possono essere visualizzati da Elaborazione report nella versione corrente. Se l'amministratore del sistema prevede di installare una nuova versione dell'elemento del report personalizzato del fornitore di software di terze parti compatibile con il nuovo formato di definizione del report, è necessario scegliere **No**. Fino a quando non diventano disponibili nuove versioni, gli elementi del report personalizzati vengono visualizzati nel report come una casella di testo vuota con una X rossa.  
  
 In entrambi i casi, il report viene aggiornato al nuovo formato di definizione del report e una copia di backup del report originale viene salvata come *\<Report Name>* `-` Backup.rdl. Se il report viene salvato nello strumento per la creazione dei report, in pratica viene salvato il report aggiornato nel nuovo formato di definizione del report. Se si pubblica il report, esso viene prima salvato nel computer, quindi pubblicato nel server di report. La versione aggiornata del report viene pubblicata nel server di report.  
  
 Se non si salva il report, il report originale resta immutato. Non è tuttavia possibile modificarlo nella versione SQL Server 2016 di [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] o in un ambiente di creazione di report in cui viene usato un formato di definizione del report più recente. È possibile continuare a eseguire la versione originale del report caricandolo in un server di report di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] tramite il portale Web. Per altre informazioni, vedere [Portale Web](../../reporting-services/web-portal-ssrs-native-mode.md).  
  
 Per i report che vengono caricati anziché pubblicati in un server di report, Elaborazione report determina se è possibile aggiornarli al primo utilizzo. I report non aggiornabili vengono elaborati in modalità di compatibilità con le versioni precedenti e continuano a essere visualizzati come nella versione precedente di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  

## <a name="next-steps"></a>Passaggi successivi

[Eseguire l'aggiornamento e la migrazione di Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Modifiche di rilievo di SQL Server Reporting Services in SQL Server 2016](../breaking-changes-in-sql-server-reporting-services-in-sql-server-2016.md)   
[Modifiche del comportamento di SQL Server Reporting Services in SQL Server 2016](../behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
[Funzionalità non più disponibili in SQL Server Reporting Services in SQL Server 2016](../../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)   
[Elementi dei report personalizzati](../../reporting-services/custom-report-items/custom-report-items.md)   
[Aggiornare un database del server di report](../../reporting-services/install-windows/upgrade-a-report-server-database.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
