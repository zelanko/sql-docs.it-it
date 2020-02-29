---
title: Eseguire la migrazione di un'installazione di Reporting Services (modalità SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 61290949-690a-4e19-b078-57c99b6b30fa
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cbfb8cf446cb95e5930ccb8178312e82db774ec3
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176961"
---
# <a name="migrate-a-reporting-services-installation-sharepoint-mode"></a>Migrazione di un'installazione di Reporting Services in modalità SharePoint
  In questo argomento viene fornita una panoramica dei passaggi necessari per eseguire la migrazione di una distribuzione in modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da un ambiente SharePoint a un altro. I passaggi specifici possono variare a seconda della versione dalla quale si esegue la migrazione. Per altre informazioni sugli scenari di aggiornamento e di migrazione per la modalità SharePoint, vedere [Upgrade and Migrate Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md). Se si vuole solo copiare gli elementi del report da un server a un altro, vedere [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md).

 Per informazioni sulla migrazione di una distribuzione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità nativa, vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).

||
|-|
|**[!INCLUDE[applies](../../includes/applies-md.md)]** SharePoint 2010 e SharePoint 2013|

 Un motivo comune per effettuare una migrazione è quando si desidera aggiornare la distribuzione di SharePoint 2010 a SharePoint 2013. SharePoint 2013 non supporta l'aggiornamento sul posto di SharePoint 2010 ed è necessario completare la procedura di **aggiornamento del collegamento di un database** o una migrazione solo del contenuto.

 Per altre informazioni sull'aggiornamento a SharePoint 2013, vedere gli argomenti seguenti:

-   [Panoramica del processo di aggiornamento a SharePoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256688).

-   [Aggiornare i database da sharepoint 2010 a sharepoint 2013](https://go.microsoft.com/fwlink/p/?LinkId=256690).

-   [Spostare i database del contenuto in SharePoint 2013](https://technet.microsoft.com/library/cc262792.aspx).

 

##  <a name="bkmk_prior_versions"></a>Eseguire la migrazione da Reporting Services versioni in modalità SharePoint precedenti al SQL Server 2012
 L'architettura della modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] modificata in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], incluso lo schema del database dell'applicazione di servizio. Se si desidera eseguire la migrazione [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] alla modalità SharePoint di da una versione [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]precedente a, creare innanzitutto il nuovo ambiente SharePoint installando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint e la modalità SharePoint di. Per ulteriori informazioni, vedere [Reporting Services installazione in modalità SharePoint &#40;sharepoint 2010 e sharepoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).

 Quando il nuovo ambiente SharePoint è in esecuzione, è possibile scegliere tra una migrazione solo del contenuto o una migrazione completa a livello di database che include i database del contenuto.

###  <a name="bkmk_content_only_migration"></a>Migrazione solo del contenuto
 **Migrazione di Reporting Services solo contenuto:** Se si desidera copiare il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] contenuto in una nuova farm, è necessario utilizzare strumenti come **RS. exe** per copiare il contenuto nella nuova installazione di SharePoint. Per altre informazioni sulle migrazioni solo del contenuto, vedere quanto riportato di seguito:

-   ** [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Script RSS:** Gli script possono eseguire la migrazione del contenuto e delle risorse tra i server di report in modalità nativa e SharePoint. Per altre informazioni, vedere [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](../tools/sample-reporting-services-rs-exe-script-to-copy-content-between-report-servers.md) e [Script di Reporting Services RS.exe che esegue la migrazione del contenuto da un server di report a un altro](https://azuresql.codeplex.com/releases/view/115207).

-   **Strumento di migrazione Reporting Services:** Lo strumento consente di copiare gli elementi del report da un server in modalità nativa a un server in modalità SharePoint. Per altre informazioni, vedere la pagina relativa allo [strumento di migrazione di Reporting Services](https://www.microsoft.com/download/details.aspx?id=29560).

###  <a name="bkmk_full_migration"></a>Migrazione completa
 **Migrazione completa:** Se si esegue la migrazione dei database del contenuto di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint insieme ai database del catalogo di a una nuova farm, è possibile seguire una serie di opzioni di backup e ripristino riepilogate in questo argomento. In alcuni casi per la fase di ripristino sarà necessario usare uno strumento diverso da quello usato per la fase di backup. È ad esempio possibile utilizzare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager per eseguire il backup delle chiavi di crittografia da [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] una versione precedente di, ma è necessario utilizzare Amministrazione centrale SharePoint o PowerShell per ripristinare le [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] chiavi di crittografia in un'installazione in modalità SharePoint.

####  <a name="bkmk_databases"></a>Database che si vedranno nella migrazione completata
 Nella tabella seguente vengono descritti i database di SQL Server correlati a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che si avranno a disposizione dopo avere eseguito correttamente la migrazione dell'installazione di SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :

|Database|Nome di esempio||
|--------------|------------------|-|
|Database del catalogo|ReportingService_ [GUID dell'applicazione di servizio] **(\*)**|L'utente esegue la migrazione.|
|Database temporaneo|ReportingService_ [GUID dell'applicazione di servizio] TempDB **(\*)**|L'utente esegue la migrazione.|
|Database di avviso|ReportingService_[GUID applicazione del servizio]_Alerting|Viene creato al momento della creazione di un'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|

 **(\*)** I nomi degli esempi illustrati nella tabella seguono la convenzione di denominazione utilizzata da SSRS quando si crea una nuova applicazione del servizio SSRS. Se si esegue la migrazione da un server diverso, i tempDB e il catalogo manterranno i nomi dall'installazione originale.

####  <a name="bkmk_backup_operations"></a>Operazioni di backup
 In questa sezione vengono descritti i tipi di informazioni necessari per eseguire la migrazione e gli strumenti o il processo da usare per completare il backup.

 ![Diagramma di base di una migrazione SharePoint per SSRS](../../../2014/sql-server/install/media/rs-sharepoint-migration.gif "Diagramma di base di una migrazione SharePoint per SSRS")

||Oggetti|Metodo|Note|
|-|-------------|------------|-----------|
|**1**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]chiavi di crittografia.|**RSKEYMGMT. exe** o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Vedere [Eseguire il backup e il ripristino delle chiavi di crittografia di Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).|Gli strumenti indicati possono essere utilizzati per il backup ma per l'operazione di ripristino saranno necessarie le pagine di gestione dell'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] oppure PowerShell.|
|**2**|Database del contenuto di SharePoint.||Creare il database e scollegarlo.<br /><br /> Vedere la sezione "Aggiornamento basato sul collegamento di database" nella pagina [Determinare il metodo di aggiornamento (SharePoint Server 2010) https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx).|
|**3**|Database di SQL Server corrispondente al database del catalogo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].|Backup e ripristino del database di SQL Server<br /><br /> o<br /><br /> Scollegamento e collegamento di un database di SQL Server.||
|**4**|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]file di configurazione.|Semplice copia di file.|È sufficiente copiare rsreportserver.config se sono state apportate personalizzazioni a tale file. Esempio di percorso predefinito dei file: C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting<br /><br /> RSReportServer.config<br /><br /> Rssvrpolicy.config<br /><br /> Web.config per l'applicazione ASP.NET del server di report.<br /><br /> Machine.config per ASP.NET.|

####  <a name="bkmk_restore_operations"></a>Operazioni di ripristino
 Questa sezione descrive i tipi di informazioni necessari per eseguire la migrazione e gli strumenti o processi da usare per completare il ripristino. È possibile che gli strumenti da usare per il ripristino siano diversi da quelli che si sono usati per il backup.

 Prima di completare i passaggi del ripristino, è necessario installare e configurare la nuova farm SharePoint e la modalità SharePoint di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per ulteriori informazioni su un'installazione di base [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] della modalità SharePoint, vedere [Reporting Services installazione in modalità sharepoint &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/install-reporting-services-sharepoint-mode.md).

||Oggetti|Metodo|Note|
|-|-------------|------------|-----------|
|**1**|Ripristinare il database del contenuto di SharePoint nella nuova farm.|Metodo SharePoint "Aggiornamento basato sul collegamento di database".|Passaggi principali:<br /><br /> 1) Ripristinare il database nel nuovo server.<br /><br /> 2) Collegare il database del contenuto a un'applicazione Web indicando l'URL.<br /><br /> 3) Get-SPWebapplication elenca tutte le applicazioni Web e tutti gli URL.<br /><br /> Vedere la sezione "Aggiornamento basato sul collegamento di database" nella pagina [Determinare il metodo di aggiornamento (SharePoint Server 2010) https://technet.microsoft.com/library/cc263447.aspx)](https://technet.microsoft.com/library/cc263447.aspx) e [Collegare database ed eseguire l'aggiornamento a SharePoint Server 2010https://technet.microsoft.com/library/cc263299.aspx)](https://technet.microsoft.com/library/cc263299.aspx) .|
|**2**|Ripristinare il database SQL che rappresenta il database del catalogo di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (ReportServer).|Backup e ripristino del database SQL.<br /><br /> **o**<br /><br /> Collegamento e scollegamento di un database di SQL Server.|Quando il database viene usato per la prima volta, in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene aggiornato lo schema del database in base alle esigenze, in modo che funzioni correttamente con l'ambiente di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .|
|**3**|Creare una nuova applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Amministrazione centrale SharePoint.|Quando si crea la nuova applicazione di servizio, configurarla per usare il database del server di report che si è copiato.<br /><br /> Per ulteriori informazioni sull'utilizzo di amministrazione centrale SharePoint, vedere la sezione "passaggio 3: creare un'applicazione di servizio Reporting Services" in [installare Reporting Services modalità SharePoint per sharepoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md).<br /><br /> Per alcuni esempi sull'uso di PowerShell, vedere la sezione "Per creare un'applicazione di servizio Reporting Services usando PowerShell" in [Reporting Services SharePoint Service and Service Applications](../../../2014/reporting-services/reporting-services-sharepoint-service-and-service-applications.md).|
|**4**|Ripristinare i file di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Semplice copia di file.|Esempio di percorso predefinito dei file: C:\Programmi\File comuni\Microsoft Shared\Web Server Extensions\15\WebServices\Reporting.|
|**5**|Ripristinare le chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .|Ripristinare il file di backup delle chiavi usando la pagina "SystemSettings" dell'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].<br /><br /> **o**<br /><br /> PowerShell.|Vedere la sezione relativa alla gestione delle chiavi nell'argomento [gestire un Reporting Services applicazione di servizio SharePoint](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md).|

#####  <a name="bkmk_additional_configuration"></a>Configurazione aggiuntiva
 A seconda di come è stato configurato l'ambiente SharePoint precedente, potrebbe essere necessario completare uno o più dei passaggi seguenti:

1.  Configurare l'autenticazione NTLM per un'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Per altre informazioni, vedere [Configurare le impostazioni di posta elettronica per l'applicazione di servizio Reporting Services &#40;SharePoint 2010 e SharePoint 2013&#41;](../../reporting-services/install-windows/configure-e-mail-for-a-reporting-services-service-application.md)

##  <a name="bkmk_migrate_from_ctp"></a>Eseguire la migrazione da una distribuzione di SQL Server 2012
 In una farm multiserver, molto probabilmente gli utenti avranno i database del contenuto e del catalogo su computer diversi, nel qual caso sarà sufficiente aggiungere alla farm di SharePoint un nuovo server con il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installato, quindi rimuovere il server obsoleto. Non è necessario copiare alcun database.

### <a name="backup-operations"></a>Operazioni di backup

1.  Eseguire il backup delle chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

2.  Eseguire il backup dell'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] tramite Amministrazione centrale SharePoint oppure utilizzare PowerShell. Ciò determinerà anche l'esecuzione del backup dei database delle applicazioni di servizio in SharePoint. Vedere l'argomento  [Eseguire il backup e il ripristino di applicazioni di servizio SharePoint di Reporting Services](../../../2014/reporting-services/backup-and-restore-reporting-services-sharepoint-service-applications.md)

3.  Se si ha un account di esecuzione automatica (UEA) e l'autenticazione di Windows, annotare le credenziali in modo da poterle usare per il processo di ripristino.

4.  Per altre informazioni, vedere [Eseguire il backup delle applicazioni di servizio in SharePoint 2013](https://technet.microsoft.com/library/ee428318.aspx).

### <a name="restore-operations"></a>Operazioni di ripristino

1.  Ripristinare l'applicazione del servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando Amministrazione centrale SharePoint. È anche possibile usare PowerShell.

2.  Ripristinare le chiavi di crittografia di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .

     Vedere la sezione "Gestione chiavi" di [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)

3.  Configurare gli account di esecuzione automatica (UEA) e credenziali di Windows sull'applicazione di servizio.

4.  Per altre informazioni, vedere [Ripristinare le applicazioni di servizio in SharePoint 2013](https://technet.microsoft.com/library/ee428305.aspx).

##  <a name="bkmk_additional_resources"></a> Risorse aggiuntive

-   [Introduzione agli aggiornamenti a SharePoint 2013 (https://technet.microsoft.com/library/ee833948.aspx)](https://technet.microsoft.com/library/ee833948.aspx).

-   [Panoramica del processo di aggiornamento a SharePoint 2013 (https://technet.microsoft.com/library/cc262483.aspx)](https://technet.microsoft.com/library/cc262483.aspx).

## <a name="see-also"></a>Vedere anche
 Eseguire l' [aggiornamento e la migrazione Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md) [eseguire la migrazione di un'installazione di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)

