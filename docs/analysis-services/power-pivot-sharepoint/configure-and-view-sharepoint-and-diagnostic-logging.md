---
title: Configurare e visualizzare SharePoint e la registrazione diagnostica | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e2df09cb9bf167c0af28c240ff69f8666cce01a6
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410418"
---
# <a name="configure-and-view-sharepoint-and-diagnostic-logging"></a>Configurare e visualizzare la registrazione diagnostica e SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] vengono registrati in file di log di SharePoint. Usare le informazioni in questo argomento per configurare i livelli di registrazione e visualizzare le informazioni sui file di log. È possibile controllare quali eventi server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] vengono registrati nel file. È inoltre possibile controllare la gravità di messaggi registrati. Per altre informazioni, vedere [Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md).  
  
 Contenuto dell'argomento:  
  
-   [Percorso del file di log](#bkmk_filelocation)  
  
-   [Modificare i livelli di registrazione diagnostica per le singole categorie di eventi](#bkmk_modifyloglevels)  
  
-   [Come visualizzare i file di log di SharePoint](#bkmk_how2viewlogfiles)  
  
##  <a name="bkmk_filelocation"></a> Percorso del file di log  
 Per impostazione predefinita, i file di log di SharePoint vengono salvati nel percorso seguente:  
  
 `C:\Program files\Common Files\Microsoft Shared\Web Server Extensions\14\LOGS`  
  
 Nella cartella LOGS sono contenuti i file di log (`.log`), i file di dati (`.txt`) e i file sull'utilizzo (`.usage`). La convenzione di denominazione dei file per un log di traccia SharePoint prevede il nome del server seguito da un timestamp con data e ora. I log di traccia SharePoint vengono creati a intervalli regolari e ogni volta che si verifica un IISRESET. È comune disporre di molti log di traccia in un periodo di 24 ore.  
  
##  <a name="bkmk_modifyloglevels"></a> Modificare i livelli di registrazione diagnostica per le singole categorie di eventi  
 Per impostazione predefinita, il livello del servizio di registrazione unificato degli eventi [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] è *Medio*. Questa impostazione è nuova per SQL Server 2012. Se è stato aggiornato un server dalla versione precedente, il livello di registrazione potrebbe ancora essere impostato su *Dettagliato*, il livello predefinito in SQL Server 2008 R2. Se si è abituati a esaminare i log del servizio di registrazione unificato per ottenere informazioni sull'utilizzo del server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , si noterà che, in conseguenza di questa modifica, è presente una quantità inferiore di informazioni sulle operazioni del server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .  
  
 Tranne che per le eccezioni, che sono di tipo *Massimo*, tutti i messaggi di [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] rientrano nella categoria Dettagliato. Se si desidera avere voci di log per operazioni di routine del server quali connessioni, richieste o report di query, è necessario modificare il livello di registrazione in Dettagliato.  
  
 Per modificare i livelli di registrazione diagnostica per le singole categorie di eventi:  
  
1.  In Amministrazione centrale SharePoint fare clic su **Monitoraggio**.  
  
2.  Fare clic su **Configura registrazione diagnostica**.  
  
3.  Scorrere fino a **Servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)]**.  
  
4.  Espandere la categoria e selezionare le singole categorie.  
  
     **Richiesta pagine applicazione** consente di specificare gli eventi attivati dall'applicazione di servizio durante l'individuazione di un'istanza di [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] per il caricamento di un'origine dati [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] e la comunicazione con altri server nella farm.  
  
     **Elaborazione richieste[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] consente di specificare gli eventi attivati da richieste di query su un database**  caricato in un server della farm.  
  
     **Utilizzo[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] consente di specificare un evento correlato alla raccolta di dati di utilizzo di** .  
  
5.  In Evento meno critico da includere nel registro eventi, selezionare **Nessuno** per disabilitare la registrazione eventi per la categoria o **Errore** per limitare la registrazione solo agli errori.  
  
6.  Selezionare **Dettagliato** per registrare tutti gli eventi nel registro eventi.  
  
7.  In Evento meno critico da includere nel registro di traccia selezionare **Nessuno** per disabilitare la traccia per la categoria o **Errore** per limitare la traccia solo agli errori.  
  
8.  Selezionare **Dettagliato** per registrare tutti gli eventi nel registro di traccia.  
  
9. Fare clic su **OK**.  
  
##  <a name="bkmk_how2viewlogfiles"></a> Come visualizzare i file di log di SharePoint  
 I file di log sono file di testo. È possibile aprirli in qualsiasi editor di testo. È inoltre possibile usare visualizzatori di log di terze parti.  
  
#### <a name="use-a-text-editor"></a>Usare un editor di testo  
 Se si usano un editor di testo per risolvere un errore del server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , i suggerimenti seguenti possono aiutare a individuare informazioni attinenti nel file:  
  
-   Per errori correlati alla pubblicazione, alla visualizzazione o all'aggiornamento di una cartella di lavoro [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] , cercare il nome della cartella di lavoro nel file di log.  
  
-   Per errori che forniscono un ID di correlazione, copiare l'ID e usarlo come termine di ricerca nel file di log.  
  
-   Cercare lo stato di errore "Elevato" o "Eccezione". Cercare "[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Service".  
  
-   Se si sa quando si è verificato l'errore, usare le informazioni sulla data e l'ora per restringere l'ambito delle voci che è necessario scorrere.  
  
#### <a name="use-a-log-viewer-application"></a>Usare un visualizzatore di log  
 Sebbene sia possibile usare un editor di testo per visualizzare singolarmente i log di traccia, un visualizzatore di log che consente di visualizzare insieme diversi file di log può essere molto più utile. Fortunatamente, sono disponibili molti visualizzatori di log di terze parti sul sito Codeplex che consentono di visualizzare più log di traccia in una sola area di lavoro.  
  
 Nelle istruzioni seguenti vengono inclusi i collegamenti ai noti visualizzatori di log ULS di SharePoint che è possibile scaricare da Codeplex.  
  
1.  Andare a [SharePoint LogViewer](http://sharepointlogviewer.codeplex.com) o [SharePoint ULS Log Viewer](http://go.microsoft.com/fwlink/?LinkId=150052) sul sito Codeplex.  
  
2.  Fare clic sulla scheda **Downloads** .  
  
3.  Fare clic sul file eseguibile. Sarà **SharePointLogViewer.exe** o **ULS Viewer 2.0 Binary**.  
  
4.  Leggere e accettare i termini di licenza.  
  
5.  Fare clic su **Save** per scaricare il software nel sistema locale.  
  
     Se si scarica il visualizzatore di log ULS di SharePoint, salvare ULSViewer.zip nella cartella Download.  
  
6.  Nella cartella Downloads fare clic con il pulsante destro del mouse su ULSViewer.zip e selezionare **Estrai tutto**.  
  
7.  Specificare una cartella di destinazione, quindi fare clic su **Extract**.  
  
8.  Nella cartella che contiene i file di programma estratti, fare doppio clic su **ULSViewer** ed eseguire l'applicazione.  
  
9. Fare clic sull'icona della cartella nell'angolo superiore sinistro della finestra dell'applicazione.  
  
10. Spostarsi su \Programmi\Common Files\Microsoft Shared\Web Server Extensions\14\Logs.  
  
11. Selezionare uno o più log di traccia. Per impostazione predefinita, i nomi dei file di log di traccia sono costituiti dal nome del computer e dalle informazioni su data e ora. Il tipo di file è Documento di testo.  
  
12. Fare clic su **Apri** e attendere il caricamento dei dati.  
  
13. Usare i filtri incorporati per selezionare i record in base a gravità, processo, categoria o file di testo definito dall'utente. È inoltre possibile fare clic sulle intestazioni di colonna per modificare l'ordinamento.  
  
#### <a name="entries-for-power-pivot-services"></a>Voci per i servizi Power Pivot  
 Nella tabella seguente sono descritte le voci per le operazioni server [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] che più probabilmente si trovano in file di log di SharePoint.  
  
|Process|Area|Category|Level|Message|Dettagli|  
|-------------|----------|--------------|-----------|-------------|-------------|  
|w3wp.exe|Servizio[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] |Uso|Dettagliato|Non sono disponibili statistiche sulle richieste, nulla da registrare.|A intervalli predefiniti, il servizio riporta le statistiche sulle risposte alle query come evento di utilizzo nel sistema di raccolta dei dati di utilizzo. Questo messaggio indica che non ci sono statistiche sulle query da riportare.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Servizio|Front-end Web|Dettagliato|Avvio individuazione server applicazioni per l'origine dati =\<*percorso*>|Quando riceve una richiesta di connessione, il servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] identifica un [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)] disponibile per gestire la richiesta. Se è presente un solo server nella farm, il server locale accetta la richiesta in tutti i casi.|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Servizio|Front-end Web|Dettagliato|Individuazione del server applicazioni riuscita.|La richiesta è stata allocata a un'applicazione di servizio [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] .|  
|w3wp.exe|[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] Servizio|Front-end Web|Dettagliato|Reindirizzamento della richiesta per il \< *origine dati PowerPivot*> per il [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)].|La richiesta è stata inoltrata a [!INCLUDE[ssGeminiSrv_md](../../includes/ssgeminisrv-md.md)].|  
|w3wp.exe|Servizio[!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] |Elaborazione delle richieste|Dettagliato|Reindirizzamento della richiesta per nomeutente\<*utente SharePoint*> al database|Una connessione rappresentata all'origine dati [!INCLUDE[ssGemini_md](../../includes/ssgemini-md.md)] è stata creata per conto dell'utente SharePoint.|  
  
## <a name="see-also"></a>Vedere anche  
 [Raccolta dati di utilizzo di PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)   
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)   
 [Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)  
  
  
