---
title: Installare, disinstallare e supporto di Generatore Report | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- administering Report Builder
ms.assetid: 2c9a5814-17bf-4947-8fb3-6269e7caa416
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: 58cd6e3180de71aff25a4ed07e3ab53c91bd5ba8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034242"
---
# <a name="install-uninstall-and-report-builder-support"></a>Installazione, disinstallazione e supporto di Generatore report
  Generatore report è uno strumento di creazione di report che consente di creare, aggiornare e condividere report, parti del report e set di dati condivisi. Generatore report è disponibile in due versioni: autonoma e [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)]. La versione autonoma viene installata nel computer in uso dall'utente o da un amministratore. La versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] viene installata automaticamente con [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] e viene scaricata nel computer da Gestione report o da un sito di SharePoint integrato con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 La versione autonoma di Generatore report non è installata con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. È necessario scaricarla e installarla separatamente da [Generatore report di Microsoft® SQL Server® 2012](https://go.microsoft.com/fwlink/?LinkId=401502).  
  
> [!NOTE]  
>  Non è possibile installare Generatore report in computer basati sul processore Itanium. Questa regola si applica sia alla versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] sia a quella autonoma di Generatore report.  
  
 In genere, un amministratore installa e configura [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], concede l'autorizzazione per utilizzare la versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] di Generatore report e gestisce cartelle e autorizzazioni per report, parti del report e set di dati condivisi salvati nel server di report. Per altre informazioni sulle [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] amministrazione, vedere [del Server di Report di Reporting Services &#40;in modalità nativa&#41; ](report-server/reporting-services-report-server-native-mode.md) nelle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [documentazione Online di](https://go.microsoft.com/fwlink/?LinkId=154888) sul sito msdn.microsoft.com.  
  
##  <a name="Installing"></a> Installazione di Generatore Report  
 Generatore report è disponibile nella versione autonoma e in quella [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] . La versione autonoma può essere scaricata e installata nel computer in uso dall'utente o dall'amministratore mentre la versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] viene installata con [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Generatore report può essere scaricato dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=186083).  
  
> [!NOTE]  
>  Generatore report non può essere installato in computer basati sul processore Itanium 64. Questa regola si applica sia alla versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] sia a quella autonoma di Generatore report.  
  
 Prima di installare una delle versioni di Generatore report, verificare i requisiti di sistema e installare qualsiasi prerequisito necessario.  
  
### <a name="system-requirements"></a>Requisiti di sistema  
 Per utilizzare Generatore report è necessario che [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] versione 3.5 sia installato nel computer locale. Se [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] non è installato nel computer locale quando si installa Generatore report, verrà richiesto di installarlo prima di poter continuare e completare l'installazione.  
  
 .NET Framework 3.5 è disponibile gratuitamente e può essere scaricato dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=110520).  
  
 Generatore report può essere installato in qualsiasi sistema operativo [!INCLUDE[msCoName](../includes/msconame-md.md)] Windows che supporti [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] 3.5, ad esempio Windows Vista o Windows 7.  
  
 È consigliabile che i computer sui quali verrà eseguito Generatore report dispongano di 512 MB di RAM. A seconda della complessità dei report che si eseguono, è tuttavia possibile utilizzare una quantità maggiore o minore di RAM.  
  
### <a name="installing-the-stand-alone-version-of-report-builder-directly-on-your-computer"></a>Installazione della versione autonoma di Generatore report direttamente nel computer in uso  
 Generatore report può essere installato dal sito di download, [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkID=186083), oppure un amministratore può rendere disponibile il file ReportBuilder3.msi, il pacchetto di Windows Installer per Generatore report, su una condivisione da cui è possibile installarlo.  
  
 È anche possibile eseguire l'installazione dalla riga di comando per includere opzioni quali, ad esempio, quelle che consentono di rendere l'installazione invisibile all'utente nonché di scrivere file di log per l'installazione. Nella documentazione relativa a Windows Installer, che consente di eseguire i file con estensione msi, vengono fornite informazioni sulle opzioni disponibili.  
  
 Per altre informazioni, vedere [installa versione di autonoma di Generatore Report &#40;Generatore Report&#41;](install-windows/install-report-builder.md).  
  
 Un amministratore può utilizzare anche un software quale Microsoft Systems Manager Server (SMS) per installare automaticamente il programma nel computer in uso. Per informazioni sull'utilizzo del software specifico per l'installazione di Generatore report, fare riferimento alla relativa documentazione.   
  
### <a name="installing-the-clickonce-version-of-report-builder-on-your-computer"></a>Installazione della versione ClickOnce di Generatore report nel computer in uso  
 La versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] di Generatore report viene installata con [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]. Viene installata sia con le installazioni native sia con quelle integrate di SharePoint di [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)].  
  
 [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] è una tecnologia Microsoft per la distribuzione di applicazioni Windows. [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] consente agli utenti di installare ed eseguire un'applicazione Windows quale Generatore report facendo clic su un collegamento in una pagina Web. Per ulteriori informazioni sulla distribuzione di applicazioni [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] , sull'applicazione della sicurezza alle applicazioni [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] o sull'esecuzione di applicazioni [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] nell'area Internet, vedere gli articoli "Distribuzione ClickOnce per applicazioni for Windows Form", "Cenni preliminari sulla sicurezza in Windows Form" o "Cenni preliminari sulla distribuzione di applicazioni attendibili" nel sito Web [!INCLUDE[msCoName](../includes/msconame-md.md)] Developer Network Web all'indirizzo [www.microsoft.com/msdn](https://www.microsoft.com/msdn).  
  
 La versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] di Generatore report si trova nel server di report e viene installata nel computer in uso quando si fa clic sul pulsante **Generatore report** in Gestione report o sull'opzione **Report di Generatore report** nel menu **Nuovo documento** in una raccolta di SharePoint.  
  
> [!NOTE]  
>  Se nel menu **Nuovo documento** non sono elencate le opzioni **Report di Generatore report**, **Modello di Generatore report**e **Origine dati report** , i relativi tipi di contenuto devono essere aggiunti alla raccolta di SharePoint.   
  
 Generatore report può essere aperto da Gestione report o da una raccolta di SharePoint. Per altre informazioni sull'apertura di Generatore Report, vedere [avviare Generatore Report &#40;Generatore Report&#41;](report-builder/start-report-builder.md).  
  
### <a name="report-builder-languages"></a>Lingue di Generatore report  
 Generatore report è disponibile in 21 lingue oltre all'inglese. Durante il download della versione autonoma di Generatore report, selezionare la lingua che si desidera installare, tenendo presente che è necessario ripetere il download per ogni lingua scelta.  
  
 Per la versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] , quando si installa [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]vengono installate tutte le lingue nel server di report. La versione localizzata installata nel computer dipende dalla lingua impostata nel computer dell'utente. Se la lingua non corrisponde a una lingua di Generatore report disponibile, verrà installata la versione in lingua inglese.  
  
 Nella tabella seguente sono riportate alcune informazioni sulle lingue disponibili.  
  
|LCID|Linguaggio|Impostazioni cultura|  
|----------|--------------|-------------|  
|1028|Cinese (tradizionale)|zh-TW|  
|1029|Ceco|cs-CZ|  
|1030|Danese|da-DK|  
|1031|Tedesco|de-DE|  
|1032|Greco|el-GR|  
|1033|Inglese|en-US|  
|1035|Finlandese|fi-FI|  
|1036|Francese|fr-FR|  
|1038|Ungherese|hu-HU|  
|1040|Italiano|it-IT|  
|1041|Giapponese|ja-JP|  
|1042|Coreano|ko-KR|  
|1043|Olandese|nl-NL|  
|1044|Norvegese (Bokmal)|nb-NO|  
|1045|Polacco|pl-PLl|  
|1046|Portoghese (Brasile)|pt-BR|  
|1049|Russo|ru-RU|  
|1053|Svedese|sv-SE|  
|1055|Turco|tr-TR|  
|2052|Cinese (semplificato)|zh-CN|  
|2070|Portoghese (Portogallo)|pt-PT|  
|3082|Spagnolo (Spagna)|es-ES|  
  
  
##  <a name="Uninstalling"></a> Disinstallazione di Generatore Report  
 È possibile disinstallare la versione autonoma di Generatore report dal Pannello di controllo o dalla riga di comando. Questa regola si applica solo alla versione autonoma di Generatore report. La versione [!INCLUDE[ndptecclick](../includes/ndptecclick-md.md)] di Generatore report non può essere disinstallata separatamente. Viene sempre installata e disinstallata con [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)].  
  
 Per altre informazioni, vedere [disinstallare stand-alone versione di Generatore Report &#40;Generatore Report&#41;](install-windows/uninstall-report-builder.md).  
  
  
##  <a name="Supporting"></a> Supporto di Generatore Report  
 Per supportare gli autori dei report, un amministratore è responsabile della gestione delle cartelle, dei report e degli elementi correlati ai report sul server di report, della concessione dell'autorizzazione alle risorse sul server di report, nonché della configurazione del server di report per l'accesso.  
  
### <a name="folders-reports-and-report-related-items"></a>Cartelle, report ed elementi correlati ai report  
 I seguenti report, elementi correlati ai report e cartelle sono gestiti sul server di report:  
  
-   Cartelle in cui vengono archiviati report, origini dati condivise, modelli e così via.  
  
-   Report personali, ovvero la cartella privata in cui vengono archiviati i report e gli elementi correlati ai report.  
  
-   Origini dati condivise che consentono agli autori dei report di utilizzare le origini dati archiviate esternamente ai report.  
  
-   Set di dati condivisi che possono fornire dati di query pronti all'uso a più report per diversi utenti.  
  
-   Parti del report quali tabelle e grafici che consentono agli utenti di migliorare e riutilizzare le parti del report, create da altri utenti, in un ambiente di collaborazione.  
  
-   Modelli del report che facilitano l'acquisizione di dati per i report da origini dati complesse.  
  
-   Immagini quali immagini di sfondo e loghi che potrebbero essere utilizzati in più report e archiviati esternamente dai report per una gestione più semplice.  
  
 Per altre informazioni, vedere [Gestione contenuto del Server di Report &#40;modalità nativa SSRS&#41; ](report-server/report-server-content-management-ssrs-native-mode.md) nelle [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [documentazione Online di](https://go.microsoft.com/fwlink/?LinkId=154888) sul sito msdn.microsoft.com.  
  
### <a name="permissions"></a>Permissions  
 L'amministratore concede l'autorizzazione al server di report. In qualità di utente di Generatore report, è necessario disporre delle autorizzazioni per il server di report prima di poter accedere al contenuto e alle funzionalità del server di report. Ad esempio potrebbe essere necessario utilizzare le parti del report archiviate nel server di report, aggiornare i report e salvarli nuovamente nel server di report, nonché eseguire i report in Gestione report. A seconda delle necessità e delle attività che si eseguono, possono essere concesse autorizzazioni di livello inferiore o superiore. Ad esempio, le autorizzazioni con privilegi minori vengono concesse agli utenti che devono solo aprire i report condivisi rispetto agli utenti che devono modificare un report condiviso.  
  
 Quando [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene installato in modalità nativa, un amministratore può:  
  
-   Abilitare la funzionalità Report personali per fornire all'utente una cartella privata per creare e salvare i report.  
  
-   Utilizzare il ruolo Generatore report sulle cartelle pubbliche per consentire all'utente di aprire una copia di un report condiviso e successivamente di salvare una versione modificata in una cartella privata.  
  
-   Utilizzare il ruolo Server di pubblicazione per consentire all'utente di gestire report e origini dati condivise nelle cartelle pubbliche. Questo ruolo è concesso agli utenti più esperti.  
  
 Quando [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] viene installato nella modalità integrata SharePoint, un amministratore può:  
  
-   Utilizzare il livello di autorizzazione di lettura, concesso al gruppo Visitatori per impostazione predefinita, per consentire all'utente di aprire una copia di un report in una cartella pubblica, quindi di salvare la versione modificata del report in una cartella privata o nel computer in uso.  
  
-   Utilizzare il livello di autorizzazione di collaborazione, concesso al gruppo Membri per impostazioni predefinita, per consentire all'utente di gestire report e origini dati condivise nelle cartelle pubbliche. Questo livello di autorizzazione è concesso agli utenti più esperti.  
  
 Per informazioni generali sulle autorizzazioni, nonché sulla creazione e sull'utilizzo dei ruoli, vedere la documentazione del [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] inclusa nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [documentazione online](https://go.microsoft.com/fwlink/?LinkId=154888)   
  
### <a name="configuration-of-report-server"></a>Configurazione del server di report  
 Quando si creano report in Generatore report e ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installata in Windows Vista, Windows Server 2008 o Windows 7, è possibile che si verifichi un errore di accesso negato quando si tenta di accedere al server di report per aprire o salvare un report. Questo errore è causato dalla funzionalità di sicurezza Controllo account utente disponibile in Windows Vista, Windows Server 2008 e Windows 7 che limita l'utilizzo eccessivo di autorizzazioni elevate rimuovendo le autorizzazioni di amministratore al momento dell'accesso alle applicazioni.  
  
 Tramite la configurazione aggiuntiva, tuttavia, il server di report è disponibile per gli utenti di Generatore report. È possibile aggiungere gli URL di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] ai siti attendibili. Per impostazione predefinita, Internet Explorer 7.0 o versioni successive viene eseguito in Modalità protetta in Windows Vista, Windows Server 2008 e Windows 7. La Modalità protetta è una funzionalità che impedisce alle richieste del browser di accedere a processi di alto livello eseguiti nello stesso computer. È possibile disabilitare la modalità protetta per le applicazioni del server di report aggiungendo le applicazioni come Siti attendibili. È necessario disporre dell'autorizzazione di amministratore per apportare questa modifica.  
  
 Per altre informazioni sulla configurazione [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], vedere [Gestione configurazione Reporting Services &#40;CANC&#41; ](/sql/2014/sql-server/install/reporting-services-configuration-manager-native-mode) nel [documentazione relativa a Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) sul sito msdn.microsoft.com.  
  
  
##  <a name="SampleDatabases"></a> Database di esempio SQL Server  
 Nella famiglia di database di esempio Adventure Works sono disponibili dati che è possibile utilizzare per ottenere informazioni sulla creazione di report e per scrivere report di esempio.  
  
 I database sono disponibili nelle versioni seguenti:  
  
-   Il database OLTP Adventure Works supporta scenari di elaborazione di transazioni online standard per un produttore di biciclette fittizio (Adventure Works Cycles). Negli scenari sono inclusi i reparti di fabbricazione, vendite, acquisti, gestione dei prodotti, gestione dei contatti e risorse umane.  
  
-   Nel database [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] viene illustrato come compilare un data warehouse.  
  
-   Il progetto [!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)] può essere utilizzato per compilare un database AS per gli scenari di Business Intelligence.  
  
 I database di esempio non sono inclusi con [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e non vengono installati quando si installa [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)] o la versione autonoma di Generatore report, possono però essere scaricati dal sito Web [CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Tutte le versioni dei database di esempio vengono scaricate insieme. È possibile anche scaricare le versioni precedenti del database rilasciate con [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)]e [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)].  
  
 Per informazioni sui prerequisiti e istruzioni sul download e sull'installazione dei database di esempio di [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , vedere le pagine relative all' [installazione dei prerequisiti per i database di esempio di SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=166648) e all' [installazione dei database di esempio](https://go.microsoft.com/fwlink/?LinkId=166649) sul sito CodePlex.  
  
  
##  <a name="HowTo"></a> Procedure  
 In questa sezione vengono elencate le procedure in cui viene illustrato come installare e disinstallare Generatore report.  
  
 [Installare la versione autonoma di Generatore Report &#40;Generatore Report&#41;](install-windows/install-report-builder.md)  
  
 [Disinstallare la versione autonoma di Generatore Report &#40;Generatore Report&#41;](install-windows/uninstall-report-builder.md)  
  
 [Avviare Generatore Report &#40;Generatore Report&#41;](report-builder/start-report-builder.md)  
  
  
## <a name="see-also"></a>Vedere anche  
 [Generatore report in SQL Server 2014](report-builder/report-builder-in-sql-server-2016.md)  
  
  
