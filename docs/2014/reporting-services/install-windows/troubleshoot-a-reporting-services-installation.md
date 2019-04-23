---
title: Risolvere i problemi di installazione di Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: e2536f7f-d90c-4571-9ffd-6bbfe69018d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c923a239ad0eeb677b476665a4c99b45d430b421
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59954207"
---
# <a name="troubleshoot-a-reporting-services-installation"></a>Risoluzione dei problemi di installazione di Reporting Services
  Se non è possibile installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a causa di errori restituiti durante l'installazione, utilizzare le indicazioni fornite in questo argomento per risolvere le condizioni che costituiscono la causa più probabile degli errori di installazione.  
  
 Per informazioni aggiornate sui problemi riguardanti [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], vedere la pagina relativa a [suggerimenti e risoluzione dei problemi di SQL Server 2012 Reporting Services](https://go.microsoft.com/fwlink/?LinkId=221297)  
  
 Per informazioni su altri errori e problemi riguardanti [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vedere la pagina relativa a [errori e risoluzione dei problemi di SSRS.](https://social.technet.microsoft.com/wiki/contents/articles/ssrs-troubleshooting-issues-and-errors.aspx)  
  
 Controllare le [note sulla versione online](https://go.microsoft.com/fwlink/?linkid=236893) per verificare se vi sia descritto il problema rilevato.  
  
 In questo argomento sono contenute le informazioni indicate di seguito.  
  
-   [Controllare i log di installazione](#bkmk_setuplogs)  
  
-   [Controllo dei prerequisiti](#bkmk_prereq)  
  
-   [Risolvere i problemi con installazioni in modalità SharePoint](#bkmk_tshoot_sharepoint)  
  
-   [Risolvere i problemi con le installazioni in modalità nativa](#bkmk_tshoot_native)  
  
-   [Risorse aggiuntive](#bkmk_additional)  
  
##  <a name="bkmk_setuplogs"></a> Verifica dei log del programma di installazione  
 Gli errori di installazione vengono registrati nel file di log di **Program Files\Microsoft SQL Server\110\Setup Bootstrap\Log** cartella. Ogni volta che si esegue il programma di installazione viene creata una sottocartella. Il nome della sottocartella è costituito dalla data e dall'ora di esecuzione del programma di installazione. Per istruzioni su come visualizzare i file di log del programma di installazione, vedere [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
-   I file di log includono una raccolta di file.  
  
-   Aprire il file *_summary.txt per visualizzare informazioni su prodotto, componente e istanza.  
  
-   Aprire il file *_errorlog.txt per visualizzare informazioni sull'errore generate durante l'installazione.  
  
-   Aprire il file *_RS\_\*_ComponentUpdateSetup.log per visualizzare informazioni sull'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
##  <a name="bkmk_prereq"></a> Verifica dei prerequisiti  
 I prerequisiti vengono verificati automaticamente dal programma di installazione. In caso di problemi relativi all'installazione, tuttavia, può essere utile conoscere i requisiti verificati dal programma di installazione.  
  
-   Tra i requisiti relativi agli account per l'esecuzione del programma di installazione è inclusa l'appartenenza al gruppo Administrators locale. Il programma di installazione deve disporre delle autorizzazioni necessarie per aggiungere file e impostazioni del Registro di sistema, creare gruppi di sicurezza locali e impostare autorizzazioni. Se si installa una configurazione predefinita, il programma di installazione deve disporre dell'autorizzazione necessaria per creare un database del server di report sull'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si esegue l'installazione.  
  
-   Il sistema operativo deve supportare HTTP.SYS 1.1.  
  
-   Il servizio HTTP deve essere abilitato e in esecuzione.  
  
-   Distributed Transaction Coordinator (DTC) deve essere in esecuzione se si intende installare anche il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   Nella cartella System32 deve essere presente il file Authz.dll.  
  
 Il programma di impostazione non verifica più la presenza di Internet Information Services (IIS) o [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] richiede MDAC 2.0 e [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] versione 2.0, che verranno installati automaticamente se non sono già presenti.  
  
##  <a name="bkmk_tshoot_sharepoint"></a> Risoluzione dei problemi relativi alle installazioni della modalità SharePoint  
  
-   [Impossibile avviare Gestione configurazione Reporting Services](#bkmk_configmanager_notstart)  
  
-   [Il servizio SQL Server Reporting Services in Amministrazione centrale SharePoint non viene visualizzato dopo l'installazione di SQL Server 2012 SSRS in modalità SharePoint](#bkmk_no_ssrs_service)  
  
-   [I cmdlet di PowerShell per Reporting Services non sono disponibili e i comandi non sono riconosciuti](#bkmk_cmdlets_not_recognized)  
  
-   [Viene visualizzato un messaggio di errore nel quale è indicato che l'URL non è configurato](#bkmk_URL_not_configured)  
  
-   [La configurazione non riesce in un computer con SharePoint installato ma non configurato](#bkmk_sharepoint_not_confiugred)  
  
-   [La pagina Amministrazione centrale SharePoint è vuota](#bkmk_central_admin_blank)  
  
-   [Viene visualizzato un messaggio di errore quando si tenta di creare un nuovo report di Generatore report](#bkmk_reportbuilder_newreport_error)  
  
-   [Viene visualizzato un messaggio di errore in cui è indicato che RS_SHP non è supportato con PREPAREIMAGE](#bkmk_RS_SHP_notsupported)  
  
###  <a name="bkmk_configmanager_notstart"></a> Impossibile avviare Gestione configurazione Reporting Services  
 **Descrizione:** Questo problema è per motivi strutturali in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è ora progettato per l'architettura del servizio SharePoint. Gestione configurazione non è più necessario per la configurazione e l'amministrazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint.  
  
 **Soluzione alternativa:** Utilizzare Amministrazione centrale SharePoint per configurare un server di report in modalità SharePoint. Per altre informazioni, vedere [Gestire un'applicazione di servizio SharePoint di Reporting Services](../../../2014/reporting-services/manage-a-reporting-services-sharepoint-service-application.md)  
  
###  <a name="bkmk_no_ssrs_service"></a> Il servizio SQL Server Reporting Services in Amministrazione centrale SharePoint non viene visualizzato dopo l'installazione di SQL Server 2012 SSRS in modalità SharePoint  
 **Descrizione:** Se dopo l'installazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint e il [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componente aggiuntivo per SharePoint 2010, non viene visualizzato "SQL Server Reporting Services" nei due menu seguenti, quindi il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio dispone di non è stato registrato:  
  
-   Amministrazione centrale SharePoint 2010 -> "Gestione applicazioni" -> pagina "Gestisci servizi nel Server"  
  
-   Amministrazione centrale SharePoint 2010 -> "Gestione applicazioni" -> "Gestisci applicazioni di servizio" -> menu "Nuovo"  
  
 **Soluzione alternativa:** Per registrare e avviare il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint Services, eseguire le operazioni seguenti:  
  
1.  Sul computer che esegue Amministrazione centrale SharePoint 2010  
  
    1.  Aprire la shell di gestione di SharePoint 2010 con privilegi di amministratore. Fare clic con il pulsante destro del mouse sull'icona e scegliere "Esegui come amministratore". Eseguire i tre cmdlet seguenti dalla shell:  
  
    2.  ```  
        Install-SPRSService  
        ```  
  
    3.  ```  
        Install-SPRSServiceProxy  
        ```  
  
    4.  ```  
        Get-SPServiceInstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
        ```  
  
2.  Verificare i [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio Mostra lo stato "**avviato**" nella pagina: SharePoint 2010 Central Administration -> "**Application Management**" -> "**Manage Services on Server**"  
  
###  <a name="bkmk_cmdlets_not_recognized"></a> I cmdlet di PowerShell per Reporting Services non sono disponibili e i comandi non sono riconosciuti  
 **Descrizione:** Quando si prova a eseguire un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] cmdlet di PowerShell, è visualizzato un messaggio di errore simile al seguente:  
  
-   Termine 'Install-SPRSServiceInstall-SPRSService' **non riconosciuto** come nome di cmdlet, funzione, programma eseguibile o file script. Controllare l'ortografia del nome, o se è stato incluso un percorso, verificare che il percorso sia corretto e riprovare. In linea: 39 char:1+ Install-SPRSServiceInstall-SPRSService <<<< + CategoryInfo: ObjectNotFound: (Installare-SPRSServiceInstall-Sprsservice) [], CommandNotFoundExcep  
  
 **Soluzione alternativa:** Completare una delle operazioni seguenti:  
  
-   Eseguire il componente aggiuntivo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per prodotti SharePoint. **rssharepoint.msi**.  
  
-   Installare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in modalità SharePoint dal supporto di installazione di SQL Server.  
  
 **Nota:** Se il **SharePoint 2013 Management Shell** è aperta quando si completare una delle soluzioni alternative, chiudere e riaprirla la shell di gestione.  
  
 Per ulteriori informazioni, vedere quanto segue:  
  
-   [Posizione in cui trovare il componente aggiuntivo Reporting Services per prodotti SharePoint](../../reporting-services/install-windows/where-to-find-the-reporting-services-add-in-for-sharepoint-products.md)  
  
-   [Installare la modalità SharePoint di Reporting Services per SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
-   [Installare Reporting Services SharePoint Mode for SharePoint 2013](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2013.md)  
  
###  <a name="bkmk_URL_not_configured"></a> Viene visualizzato un messaggio di errore nel quale è indicato che l'URL non è configurato  
 **Descrizione:** Viene vedere messaggio di errore simile al seguente:  
  
 Questa funzionalità di SQL Server Reporting Services (SSRS) non è supportata. Utilizzare Amministrazione centrale per verificare e correggere uno o più dei seguenti problemi:•L'URL di un server di report non è configurato. Utilizzare la pagina Integrazione di SSRS per impostarlo.•Il proxy dell'applicazione del servizio SSRS non è configurato. Utilizzare le pagine relative all'applicazione del servizio SSRS per configurare il proxy.•Non è stato eseguito il mapping dell'applicazione del servizio SSRS a questa applicazione Web. Utilizzare le pagine relative all'applicazione del servizio SSRS per associare il proxy dell'applicazione del servizio Web al gruppo di proxy dell'applicazione per questa applicazione Web.  
  
 **Soluzione alternativa:** Il messaggio di errore contiene tre passaggi suggeriti per correggere questo problema. Il primo suggerimento nel messaggio 'Un server di report URL non è configurato..' è pertinente per l'integrazione con la versione del server di report anteriore a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. La configurazione di SharePoint per le versioni del server di report precedenti viene completata nella pagina **Impostazioni generali applicazione** usando **SQL Server Reporting Services (2008 e 2008 R2)**.  
  
 **Altre informazioni:** Si verrà visualizzato questo messaggio di errore quando provano a usare uno qualsiasi dei [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] funzionalità che richiedono una connessione al [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio. ad esempio:  
  
-   Apertura di Generatore report di SQL Server da una raccolta documenti di SharePoint.  
  
-   Gestione di sottoscrizioni.  
  
-   Gestione di un'applicazione di servizio  
  
###  <a name="bkmk_sharepoint_not_confiugred"></a> La configurazione non riesce in un computer con SharePoint installato ma non configurato  
 **Descrizione:** Se si seleziona per installare Reporting Services SharePoint Mode su un computer con SharePoint installato ma SharePoint non è configurato, verrà visualizzato che un messaggio simile al seguente e l'installazione viene arrestata:  
  
 L'installazione di SQL Server ha smesso di funzionare  
  
 **Soluzione alternativa:** Configurare SharePoint ed eseguire l'installazione di SQL Server.  
  
 **Altre informazioni:** Quando si installa [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in e un'installazione di SharePoint, il programma di installazione tenta di installare e avviare il [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servizio SharePoint. L'installazione del servizio non riesce se SharePoint non è configurato.  
  
###  <a name="bkmk_central_admin_blank"></a> La pagina Amministrazione centrale SharePoint è vuota  
 **Descrizione:** Era stato installato SharePoint 2010, senza errori. Tuttavia quando si passa ad Amministrazione centrale, viene visualizzata una pagina vuota.  
  
 **Soluzione alternativa:** Questo problema non riguarda [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ma è relativo alla configurazione delle autorizzazioni nell'installazione generale di SharePoint. Di seguito viene fornito un elenco di suggerimenti:  
  
-   Esaminare l'argomento relativo a SharePoint negli ambienti di sviluppo. [Configurazione dell'ambiente di sviluppo per SharePoint 2010 in Windows Vista, Windows 7 e Windows Server 2008](https://msdn.microsoft.com/library/ee554869\(office.14\).aspx)  
  
-   Esaminare il post del forum: [Amministrazione centrale restituisce una pagina vuota dopo l'installazione in Windows 7](https://social.technet.microsoft.com/Forums/en/sharepoint2010setup/thread/a422a3c8-39f6-4b9e-988a-4c4d1e745694)  
  
-   L'account del servizio che si sta utilizzando per i servizi SharePoint, ad esempio il servizio Amministrazione centrale SharePoint 2010, deve disporre dei privilegi amministrativi nel sistema operativo locale.  
  
###  <a name="bkmk_reportbuilder_newreport_error"></a> Viene visualizzato un messaggio di errore quando si tenta di creare un nuovo report di Generatore report  
 **Descrizione:** Quando si prova a creare un report di Generatore Report all'interno di una raccolta documenti, viene visualizzato un messaggio di errore simile al seguente:  
  
 Questa funzionalità non è supportata perché non esiste un'applicazione del servizio SQL Server Reporting Services o non è stato configurato un URL del server di report in Amministrazione centrale.  
  
 **Soluzione alternativa:** Verificare avere un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] applicazione di servizio e sia configurato correttamente. Per altre informazioni, vedere la sezione "creare un'applicazione di servizio Reporting Services" in [installare Reporting Services SharePoint Mode for SharePoint 2010](../../../2014/sql-server/install/install-reporting-services-sharepoint-mode-for-sharepoint-2010.md)  
  
###  <a name="bkmk_RS_SHP_notsupported"></a> Viene visualizzato un messaggio di errore in cui è indicato che RS_SHP non è supportato con PREPAREIMAGE  
 **Descrizione:** Quando si tenta di eseguire PREPAREIMAGE per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene visualizzato un messaggio di errore simile al seguente:  
  
 "Funzionalità specificata 'RS_SHP' non supportata durante l'esecuzione dell'azione PREPAREIMAGE perché l'utilità SysPrep non è supportata. Rimuovere le funzionalità non compatibili con SysPrep ed eseguire nuovamente l'installazione".  
  
 **Soluzione alternativa:** Non vi è alcuna soluzione alternativa. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non supporta SYSPREP (PREPAREIMAGE). [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non supporta SYSPREP.  
  
##  <a name="bkmk_tshoot_native"></a> Risoluzione dei problemi relativi alle installazioni della modalità nativa  
  
###  <a name="PerfCounters"></a> I contatori delle prestazioni non sono visibili al termine dell'aggiornamento a Windows Vista o Windows Server 2008  
 Se si aggiorna il sistema operativo a [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] o [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] in un computer che esegue [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], i contatori delle prestazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non verranno impostati dopo l'aggiornamento.  
  
#### <a name="to-reinstate-reporting-services-performance-counters"></a>Per riattivare i contatori delle prestazioni di Reporting Services  
  
1.  Eliminare le chiavi del Registro di sistema seguenti:  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service**  
  
    -   **HKLM\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service**  
  
2.  Aprire una finestra del prompt dei comandi e digitare il comando seguente:  
  
    -   **eseguire \<**  *directory .NET 2.0 Framework* **> \InstallUtil.exe \<**  *directory Bin Server di Report* **> \ReportingServicesLibrary.dll**  
  
        > [!NOTE]  
        >  Sostituire \< *directory .NET 2.0 Framework*> con il percorso fisico di .NET Framework 2.0 file e sostituire \< *directory Bin Server di Report*> con il percorso fisico del file della cartella bin server di report.  
  
3.  Riavviare il servizio [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Per verificare che il problema sia stato risolto, aprire un browser e accedere all'URL di Gestione report o del server di report. Aprire quindi Performance Monitor per verificare che i contatori funzionino correttamente.  
  
#### <a name="to-re-add-the-performance-registry-keys-by-using-registry-editor"></a>Per aggiungere nuovamente le chiavi del Registro di sistema delle prestazioni utilizzando l'editor del Registro di sistema  
  
1.  Aprire l'editor del Registro di sistema.  
  
    1.  Fare clic su **Start**e scegliere **Esegui**.  
  
    2.  Nel **eseguiti** nella finestra di dialogo il **Open** digitare `regedit`.  
  
2.  Nell'editor del Registro di sistema, selezionare la seguente chiave del Registro di sistema: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
3.  Fare clic con il pulsante destro del mouse sul nodo **Prestazioni** , scegliere **Nuovo**e fare clic su **Valore multistringa**.  
  
4.  Digitare `Counter Names` e quindi premere INVIO.  
  
5.  Ripetere il passaggio per aggiungere la chiave del Registro di sistema `Counter Types` in questo nodo.  
  
6.  Passare alla chiave del Registro di sistema seguente: `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance`  
  
7.  Fare clic con il pulsante destro del mouse sul nodo **Prestazioni** , scegliere **Nuovo**e fare clic su **Valore multistringa**.  
  
8.  Digitare `Counter Names` e quindi premere INVIO.  
  
9. Ripetere il passaggio per aggiungere la chiave del Registro di sistema `Counter Types` in questo nodo.  
  
 Dopo aver ripristinato l'istanza a 64 bit o aggiunto nuovamente le chiavi del Registro di sistema manualmente, è possibile utilizzare Performance Monitor per configurare gli oggetti prestazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da monitorare.  
  
###  <a name="ConfigPropsMissing"></a> Le proprietà di configurazione ReportServerExternalURL e PassThroughCookies non sono configurate dopo un aggiornamento da SQL Server 2005  
 Quando si esegue l'aggiornamento da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], le proprietà di configurazione `ReportServerExternalURL` e `PassThroughCookies` non vengono configurate dal processo di aggiornamento. `ReportServerExternalURL` proprietà facoltativa e deve essere impostata solo se si usa Web part di SharePoint 2.0 e si desidera che gli utenti siano in grado di recuperare un report e aprirlo in una nuova finestra del browser. Per altre informazioni sulle `ReportServerExternalURL`, vedere [URL nei file di configurazione &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/urls-in-configuration-files-ssrs-configuration-manager.md). `PassThroughCookies` è necessario solo quando si usa il metodo di autenticazione personalizzato. Per altre informazioni sulle `PassThroughCookies`, vedere [configurare Gestione Report per il passaggio di cookie di autenticazione personalizzati](../security/configure-the-web-portal-to-pass-custom-authentication-cookies.md).  
  
> [!NOTE]  
>  Quando si utilizza l'autenticazione personalizzata, si consiglia di eseguire la migrazione dell'installazione anziché un aggiornamento. Per altre informazioni sulla migrazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Eseguire la migrazione di un'installazione di Reporting Services &#40;modalità nativa&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md).  
  
 Per impostazione predefinita, queste proprietà non esistono nella configurazione di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] . Se queste proprietà sono state configurate in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e le funzionalità che forniscono continuano ad essere richieste, è necessario aggiungerle manualmente al file **RSReportServer.config** dopo il processo di aggiornamento. Per altre informazioni, vedere [Modificare un file di configurazione di Reporting Services&#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md).  
  
###  <a name="Default2005InstallBreaks2008"></a> Si verifica un errore di installazione per un'istanza predefinita di SQL Server 2005 Reporting Services in un computer che esegue SQL Server 2012 Reporting Services  
 Se si tenta di installare un'istanza predefinita di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in un computer che già esegue un'istanza di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], l'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non verrà installata e verrà restituito il messaggio di errore seguente:  
  
 "Un'istanza con lo stesso nome è già installata nel computer. Per continuare l'installazione di SQL Server, specificare un nome di istanza univoco".  
  
 Questo problema si verifica a prescindere se l'istanza di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] è predefinita o denominata e a prescindere se un'istanza di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] con quel nome esiste già nel computer.  
  
 Per risolvere questo problema, effettuare una delle operazioni seguenti:  
  
-   Se è necessario eseguire [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] come l'istanza predefinita del computer, è necessario installare l'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] prima dell'istanza di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
-   Se l'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non deve necessariamente essere l'istanza predefinita, è possibile installare l'istanza di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] come un'istanza denominata dopo l'installazione dell'istanza di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] .  
  
###  <a name="WindowsAuthBreaksAfterUpgrade"></a> Errore 401 quando si usa l'autenticazione di Windows dopo un aggiornamento da SQL Server 2005 a SQL Server 2012  
 Se si esegue l'aggiornamena da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)]e si usa l'autenticazione NTLM con un account predefinito per l'account del servizio del server di report, è possibile che si verifichi l'errore 401 di autorizzazione negata quando si accede al server di report o a Gestione report dopo l'aggiornamento.  
  
 L'errore si verifica a causa di una modifica nella configurazione predefinita di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] per l'autenticazione di Windows. La negoziazione viene configurata quando l'account del servizio del server di report è Servizio di rete o Sistema locale. L'autenticazione NTLM viene configurata quando l'account del servizio del server di report non è un account predefinito. Per risolvere questo problema dopo l'aggiornamento, modificare il file RSReportServer.config e configurare `AuthenticationType` su `RSWindowsNTLM`. Per altre informazioni, vedere [Configurare l'autenticazione di Windows nel server di report](../security/configure-windows-authentication-on-the-report-server.md).  
  
###  <a name="Uninstall32BitBreaks64Bit"></a> La disinstallazione dell'istanza a 32 bit di SQL Server 2012 Reporting Services in una distribuzione side-by-side con un'istanza a 64 bit interrompe l'a 64 bit istanza  
 Quando si esegue l'installazione side-by-side di un'istanza a 32 bit e di un'istanza a 64 bit di [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] in un computer e si disinstalla l'istanza a 32 bit, quattro chiavi del Registro di sistema di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] vengono rimosse. e di conseguenza, l'istanza a 64 bit di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]viene interrotta. Le chiavi del Registro di sistema di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] che vengono rimosse quando si disinstalla l'istanza a 32 bit sono:  
  
 `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Names` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Web Service\Performance:Counter Types` `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MSRS 2011 Windows Service\Performance:Counter Types`  
  
 Per risolvere questo problema, è possibile ripristinare l'istanza a 64 bit. Sebbene il ripristino sia l'operazione consigliata, è comunque possibile aggiungere nuovamente le chiavi del Registro di sistema manualmente utilizzando l'editor del Registro di sistema.  
  
> [!CAUTION]  
>  Se il Registro di sistema viene modificato in modo non appropriato, il sistema potrebbe venire gravemente danneggiato. Prima di modificare il Registro di sistema, è consigliabile eseguire il backup di tutti i dati importanti disponibili nel computer.  
  
##  <a name="bkmk_additional"></a> Risorse aggiuntive  
 Di seguito sono riportate ulteriori risorse disponibili per la risoluzione dei problemi:  
  
-   Wiki di TechNet: Negli argomenti di risoluzione dei problemi [risolvere i problemi di SQL Server Reporting Services (SSRS) in modalità integrata SharePoint](https://social.technet.microsoft.com/wiki/contents/articles/troubleshoot-sql-server-reporting-services-ssrs-in-sharepoint-integrated-mode.aspx)  
  
-   [Forum: SQL Server Reporting Services](http://social.msdn.microsoft.com/Forums/sqlreportingservices/threads)  
  
 ![Impostazioni di SharePoint](../../../2014/analysis-services/media/as-sharepoint2013-settings-gear.gif "impostazioni SharePoint") [Invia commenti e suggerimenti e informazioni di contatto tramite Microsoft SQL Server Connect](https://connect.microsoft.com/SQLServer/Feedback) (https://connect.microsoft.com/SQLServer/Feedback).  
  
  
