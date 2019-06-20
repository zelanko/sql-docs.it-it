---
title: Sottoscrizioni e recapito (Reporting Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- reports [Reporting Services], distributing
- distributing reports [Reporting Services]
- published reports [Reporting Services], distributing
- sending reports
- sharing reports
- delivering reports [Reporting Services]
- distributing reports [Reporting Services], subscriptions
- subscriptions [Reporting Services], about subscriptions
- subscriptions [Reporting Services]
ms.assetid: be7ec052-28e2-4558-bc09-8479e5082926
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f598946ec6231d1ca5edacf1810431beb4638f88
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66100665"
---
# <a name="subscriptions-and-delivery-reporting-services"></a>Subscriptions and Delivery (Reporting Services)
  Una sottoscrizione di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] è una configurazione che recapita un report in un momento specifico o in risposta a un evento e in un formato file specificato. Ad esempio, è possibile salvare il report MonthlySales.rdl ogni mercoledì come documento di Microsoft Word in una condivisione file. Le sottoscrizioni possono essere usate per pianificare e automatizzare il recapito di un report e con un set specifico di valori di parametri di report.  
  
 È possibile creare più sottoscrizioni per un singolo report per usare opzioni di sottoscrizione diverse. Si potrebbero specificare valori diversi per i parametri in modo da creare tre versioni di un report, ad esempio un report delle vendite per le regioni centro-settentrionali, un report delle vendite per le regioni centro-meridionali e un report relativo a tute le vendite.  
  
 ![esempio di flusso di sottoscrizione ssrs](../media/ssrs-subscription-example-flow.png "esempio di flusso di sottoscrizione ssrs")  
  
 Le sottoscrizioni non sono disponibili in tutte le edizioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
> [!NOTE]
>  A partire da [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], è possibile trasferire la proprietà di una sottoscrizione a livello di programmazione. Non è disponibile alcuna interfaccia utente da utilizzare per trasferire la proprietà delle sottoscrizioni. Per altre informazioni, vedere <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>e [usare PowerShell per modificare ed elenco Reporting Services Subscription Owners and Run a Subscription](manage-subscription-owners-and-run-subscription-powershell.md).  
  
 **Contenuto dell'argomento:**  
  
-   [Sottoscrizione e gli scenari di distribuzione](#bkmk_subscription_scenarios)  
  
-   [Sottoscrizioni standard e guidate dai dati](#bkmk_standard_and_datadriven)  
  
-   [Requisiti della sottoscrizione](#bkmk_subscription_requirements)  
  
-   [Estensioni per il recapito](#bkmk_delivery_extensions)  
  
-   [Parti di una sottoscrizione](#bkmk_parts_of_subscription)  
  
-   [Procedura di elaborazione delle sottoscrizioni](#bkmk_subscription_processing)  
  
-   [Procedura di elaborazione delle sottoscrizioni](#bkmk_subscription_processing)  
  
 **Contenuto della sezione:**  
  
-   [Recapito tramite posta elettronica in Reporting Services](e-mail-delivery-in-reporting-services.md) Descrive la configurazione e il funzionamento del recapito tramite posta elettronica gestito dal server di report.  
  
-   [File Share Delivery in Reporting Services](file-share-delivery-in-reporting-services.md) Descrive la configurazione e il funzionamento del recapito tramite condivisione file gestito dal server di report.  
  
-   [SharePoint Library Delivery in Reporting Services](sharepoint-library-delivery-in-reporting-services.md) Descrive il recapito della sottoscrizione a una raccolta di SharePoint.  
  
-   [Sottoscrizioni guidate dai dati](data-driven-subscriptions.md) Fornisce informazioni sulle sottoscrizioni guidate dai dati per la personalizzazione dell'output dei report in fase di esecuzione.  
  
-   [Creare e gestire sottoscrizioni per server di report in modalità nativa](../create-manage-subscriptions-native-mode-report-servers.md)  
  
-   [Creare e gestire sottoscrizioni per server di report in modalità SharePoint](create-and-manage-subscriptions-for-sharepoint-mode-report-servers.md)  
  
-   [Monitorare le sottoscrizioni di Reporting Services](monitor-reporting-services-subscriptions.md)  
  
-   [Usare PowerShell per modificare ed elencare i proprietari di sottoscrizioni di Reporting Services ed eseguire una sottoscrizione](manage-subscription-owners-and-run-subscription-powershell.md)  
  
##  <a name="bkmk_subscription_scenarios"></a> Sottoscrizione e gli scenari di distribuzione  
 È possibile configurare le opzioni di recapito per ogni sottoscrizione e le opzioni disponibili sono determinate dall'estensione di recapito scelta. Un'estensione per il recapito è un modulo che supporta alcune modalità di distribuzione. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] include alcune estensioni di recapito e terze parti potrebbero mettere a disposizione estensioni aggiuntive.  
  
 Uno sviluppatore può creare estensioni per il recapito personalizzate per supportare scenari aggiuntivi. Per altre informazioni, vedere [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
 Nella tabella seguente sono descritti gli scenari di sottoscrizione di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] più comuni.  
  
|Scenario|Descrizione|  
|--------------|-----------------|  
|Invia report tramite posta elettronica|Inviare report tramite posta elettronica a singoli utenti e gruppi. Creare una sottoscrizione e specificare un alias di gruppo o un alias di posta elettronica per ricevere un report che si desidera distribuire. È possibile che [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] determini in fase di esecuzione i dati della sottoscrizione. Per inviare lo stesso report a un gruppo che dispone di un elenco di membri che cambia, è possibile utilizzare una query per dedurre in fase di esecuzione l'elenco delle sottoscrizioni.|  
|Visualizzare i report offline|È possibile inviare i report da archiviare direttamente a una cartella condivisa della quale si esegue il backup in una pianificazione notturna. I report di grandi dimensioni che impiegano troppo lungo per il caricamento in un browser possono essere inviati a una cartella condivisa in un formato che può essere visualizzato in un'applicazione desktop. Gli utenti possono selezionare uno dei formati seguenti per l'output della sottoscrizione:<br /><br /> File XML con dati del report<br /><br /> CSV (delimitato da virgole)<br /><br /> PDF<br /><br /> MHTML (archivio Web)<br /><br /> Microsoft Excel<br /><br /> File TIFF<br /><br /> Microsoft Word|  
|Cache di pre-caricamento|Se sono disponibili più istanze di un report con parametri o di un gran numero di utenti che visualizzano report, è possibile precaricare i report nella cache per ridurre il tempo di elaborazione necessario per visualizzare il report.|  
|Report guidati dai dati|Utilizzare le sottoscrizioni guidate dai dati per personalizzare in fase di esecuzione l'output del report, le opzioni di recapito e le impostazioni dei parametri del report. La sottoscrizione utilizza una query per ottenere in fase di esecuzione i valori di input da un'origine dati. È possibile utilizzare le sottoscrizioni guidate dai dati per eseguire un'operazione di merge della posta elettronica che invia un report a un elenco di sottoscrittori determinato al momento dell'elaborazione della sottoscrizione.|  
  
##  <a name="bkmk_standard_and_datadriven"></a> Sottoscrizioni standard e guidate dai dati  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] supporta due tipi di sottoscrizione, vale a dire **standard** e **guidata dai dati**. Le sottoscrizioni standard vengono create e gestite da singoli utenti. Una sottoscrizione standard è costituita da valori statici, che non possono essere modificati durante l'elaborazione della sottoscrizione. Per ogni sottoscrizione standard esiste un solo set di opzioni di presentazione del report, opzioni di recapito e parametri del report.  
  
 Le sottoscrizioni guidate dai dati ottengono informazioni sulla sottoscrizione in fase di esecuzione eseguendo una query su un'origine dati esterna che fornisce valori utilizzati per specificare un destinatario, parametri del report o formato dell'applicazione. È possibile utilizzare le sottoscrizioni guidate dai dati se si dispone di un elenco di destinatari molto esteso o si desidera modificare l'output del report per ogni destinatario. Per utilizzare le sottoscrizioni guidate dai dati è necessario essere in grado di compilare query e sapere come vengono utilizzati i parametri. Le sottoscrizioni guidate dai dati vengono in genere create e gestite dagli amministratori dei server di report. Per ulteriori informazioni, vedere quanto segue:  
  
-   [Sottoscrizioni guidate dai dati](data-driven-subscriptions.md)  
  
-   [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)  
  
##  <a name="bkmk_subscription_requirements"></a> Requisiti della sottoscrizione  
 Per poter creare una sottoscrizione di un report, è innanzitutto necessario che siano soddisfatti i requisiti seguenti:  
  
|Requisito|Descrizione|  
|-----------------|-----------------|  
|Permissions|È necessario poter accedere al report. Per poter sottoscrivere un report, è necessario disporre delle autorizzazioni necessarie per visualizzarlo.<br /><br /> L'assegnazione di ruolo deve includere l'attività Gestione di sottoscrizioni individuali.|  
|Credenziali archiviate.|Per creare una sottoscrizione, è necessario che per il report siano usate credenziali archiviate oppure nessuna credenziale per poter recuperare i dati in fase di esecuzione. Non è possibile sottoscrivere un report configurato per utilizzare credenziali rappresentate o delegate dell'utente corrente per connettersi a un'origine dati esterna. Le credenziali archiviate possono essere un account di Windows o un account utente del database. Per altre informazioni, vedere [Specificare le credenziali e le informazioni sulla connessione per le origini dati del report](../report-data/specify-credential-and-connection-information-for-report-data-sources.md)<br /><br /> e si dispone delle autorizzazioni necessarie per visualizzare il report e creare sottoscrizioni individuali. È necessario che l'opzione**Eventi pianificati e recapito report** sia abilitata sul server di report. Per altre informazioni, vedere [Creare e gestire sottoscrizioni per server di report in modalità nativa](../create-manage-subscriptions-native-mode-report-servers.md).|  
|Valori dipendenti dall'utente in un report|Per le sole sottoscrizioni standard è possibile creare sottoscrizioni a report in cui le informazioni sull'account utente sono incluse in un filtro o sono disponibili sotto forma di testo visualizzato nel report. Nel report il nome dell'account utente viene specificato tramite un'espressione `User!UserID` che corrisponde all'utente corrente. Quando si crea una sottoscrizione, l'autore della sottoscrizione viene considerato come utente corrente.|  
|Nessuna sicurezza degli elementi del modello|Non è possibile sottoscrivere un report di Generatore report che utilizza come origine dei dati un modello contenente impostazioni di sicurezza degli elementi del modello. La restrizione riguarda solo i report che utilizzano la sicurezza degli elementi del modello.|  
|Valori dei parametri|Se il report utilizza parametri, è necessario specificare un valore di parametro con il report stesso oppure nella sottoscrizione che viene definita. Se nel report sono stati specificati valori predefiniti, è possibile impostare il valore di parametro per utilizzare l'impostazione predefinita.|  
  
##  <a name="bkmk_delivery_extensions"></a> Estensioni per il recapito  
 Le sottoscrizioni vengono elaborate sul server di report e distribuite mediante estensioni per il recapito distribuite sul server. Per impostazione predefinita, è possibile creare sottoscrizioni che inviano report a una cartella condivisa oppure a un indirizzo di posta elettronica. È possibile inviare un report a una raccolta di SharePoint se il server di report è configurato per la modalità integrata SharePoint.  
  
 Al momento della creazione di una sottoscrizione, gli utenti hanno la possibilità di scegliere una delle estensioni per il recapito disponibili che determinano la modalità di recapito del report. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] sono disponibili le estensioni per il recapito seguenti.  
  
|Estensione per il recapito|Descrizione|  
|------------------------|-----------------|  
|Condivisione file di Windows|Consente di recapitare un report come file di applicazione statico a una cartella condivisa cui è possibile accedere sulla rete.|  
|Posta elettronica|Consente di recapitare una notifica o un report come un allegato della posta elettronica o un collegamento URL.|  
|Raccolta di SharePoint|Consente di recapitare un report come file di applicazione statico a una raccolta di SharePoint cui è possibile accedere da un sito di SharePoint. Il sito deve essere integrato con un server di report in esecuzione in modalità integrata SharePoint.|  
|Null|Il provider di recapito Null è un'estensione per il recapito estremamente specializzata utilizzata per precaricare una cache con report con parametri immediatamente visualizzabile. Questo metodo non è disponibile per sottoscrizioni individuali. Il recapito Null viene utilizzato dagli amministratori in sottoscrizioni guidate dai dati per l'ottimizzazione delle prestazioni del server di report mediante il precaricamento della cache.|  
  
> [!NOTE]  
>  Il recapito di report è una parte estendibile dell'architettura di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Altri fornitori possono creare estensioni per il recapito personalizzate per inviare report a posizioni o dispositivi diversi. Per ulteriori informazioni sulle estensioni per il recapito personalizzate, vedere [Implementing a Delivery Extension](../extensions/delivery-extension/implementing-a-delivery-extension.md).  
  
##  <a name="bkmk_parts_of_subscription"></a> Parti di una sottoscrizione  
 La definizione di una sottoscrizione è costituita dagli elementi seguenti:  
  
-   Un puntatore a un report che può essere eseguito in modo automatico, ovvero un report che utilizza credenziali archiviate o che non ne utilizza alcuna.  
  
-   Una modalità di recapito (ad esempio tramite posta elettronica) e le impostazioni per la modalità di recapito (ad esempio un indirizzo di posta elettronica).  
  
-   Un'estensione per il rendering per la presentazione del report in un formato specifico.  
  
-   Le condizioni per l'elaborazione della sottoscrizione, che vengono espresse come evento.  
  
     In genere, le condizioni per l'esecuzione di un report si basano sul tempo. Se ad esempio si desidera eseguire un particolare report ogni martedì alle 15.00 (ora UTC) e il report è configurato per l'esecuzione come snapshot, è possibile specificare che la sottoscrizione deve essere eseguita tutte le volte in cui lo snapshot viene aggiornato.  
  
-   I parametri utilizzati durante l'esecuzione del report.  
  
     I parametri sono facoltativi e vengono specificati solo per report che accettano valori di parametro. Dato che una sottoscrizione è in genere di proprietà di un utente, i valori di parametro che vengono specificati variano da sottoscrizione a sottoscrizione. Ad esempio, i responsabili delle vendite per reparti diversi utilizzeranno parametri che restituiscono dati per il proprio reparto. Per ogni parametro deve essere definito un valore in modo esplicito oppure deve essere impostato un valore predefinito valido.  
  
 Le informazioni relative alle sottoscrizioni vengono archiviate con ogni report in un database del server di report. Non è possibile gestire le sottoscrizioni separatamente dal report al quale sono associate. Si noti che non è possibile integrare le sottoscrizioni con descrizioni o altro tipo di testo personalizzato né con altri elementi. Le sottoscrizioni possono contenere solo gli elementi elencati in precedenza.  
  
##  <a name="bkmk_subscription_processing"></a> Procedura di elaborazione delle sottoscrizioni  
 [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] include il componente Elaborazione pianificazione e recapito che offre funzionalità per la pianificazione e il recapito di report agli utenti. Il server di report risponde a eventi di cui esegue costantemente il monitoraggio. Quando viene generato un evento che corrisponde alle condizioni definite per una sottoscrizione, il server di report accede alle impostazioni della sottoscrizione per determinare come elaborare e recapitare il report. Il server di report richiede l'estensione per il recapito specificata nella sottoscrizione. Quando l'estensione per il recapito è in esecuzione, il server di report estrae le informazioni relative al recapito dalla sottoscrizione e le passa per l'elaborazione all'estensione per il recapito.  
  
 L'estensione per il recapito esegue il rendering del report nel formato definito nella sottoscrizione e recapita il report o la notifica alla destinazione specificata. Se un report non può essere recapitato, viene registrata una voce specifica nel file di log del server di report. Se si desidera che siano supportate operazioni di riesecuzione dei tentativi, è possibile configurare il server di report in modo che tenti di rieseguire il recapito se il primo tentativo non riesce.  
  
### <a name="processing-a-standard-subscription"></a>Elaborazione di una sottoscrizione standard  
 Le sottoscrizioni standard generano una sola istanza di un report. Il report viene recapitato a un'unica cartella condivisa o agli indirizzi di posta elettronica specificati nella sottoscrizione. I dati e il layout del report rimangono invariati. Se per il report vengono utilizzati parametri, viene elaborata una sottoscrizione standard con un solo valore per ogni parametro del report.  
  
### <a name="processing-a-data-driven-subscription"></a>Elaborazione di una sottoscrizione guidata dai dati  
 Le sottoscrizioni guidate dai dati possono essere impostate in modo da generare numerose istanze di un report che verranno recapitate a più destinazioni. Il layout del report non varia, tuttavia i dati del report possono variare se vengono passati valori dei parametri da un set di risultati del sottoscrittore. Le opzioni di recapito che hanno effetto sul formato di rendering del report e sulle modalità di trasferimento del report stesso, ovvero se viene allegato o collegato al messaggio di posta elettronica, possono variare anche in base al sottoscrittore quando i valori vengono passati dal set di righe.  
  
 Le sottoscrizioni guidate dai dati possono generare numerose operazioni di recapito. Il server di report crea un'operazione di recapito per ogni riga del set di righe restituito dalla query di sottoscrizione.  
  
### <a name="report-delivery-characteristics"></a>Caratteristiche del recapito di report  
 Con le sottoscrizioni standard i report vengono in genere recapitati come report statici. Questi report si basano sullo snapshot dell'esecuzione del report più recente oppure vengono generati come report statici allo scopo di completare un'operazione di recapito. Se si seleziona l'opzione **Includi collegamento** in una sottoscrizione di un report che viene eseguito su richiesta, il server di report eseguirà il report quando si fa clic sul collegamento ipertestuale.  
  
> [!NOTE]  
>  I report che vengono recapitati mediante l'invio dell'URL rimangono connessi al server di report e possono pertanto venire aggiornati o eliminati dopo il recapito. Le opzioni di recapito selezionate per la sottoscrizione determinano se il report viene recapitato come URL, incorporato in un messaggio di posta elettronica o inviato come allegato a un messaggio.  
  
 I report recapitati tramite una sottoscrizione guidata dai dati potrebbero essere generati di nuovo durante l'elaborazione della sottoscrizione. Per completare una sottoscrizione guidata dai dati, il server di report non si limita a utilizzare un'istanza specifica del report e del relativo set di dati. Se la sottoscrizione utilizza valori dei parametri diversi per diversi sottoscrittori, il server di report genera di nuovo il report per produrre il risultato richiesto. Se i dati sottostanti vengono aggiornati dopo la creazione e il recapito della prima copia del report, gli utenti che riceveranno il report in una fase successiva del processo potrebbero visualizzare dati basati su un set di risultati diverso. È possibile utilizzare un report eseguito come snapshot per assicurare che la stessa istanza del report venga recapitata a tutti i sottoscrittori. Se tuttavia durante l'elaborazione della sottoscrizione si verifica un aggiornamento pianificato dello snapshot, nei report ricevuti da utenti diversi potrebbero comunque essere disponibili dati diversi.  
  
### <a name="triggering-subscription-processing"></a>Attivazione dell'elaborazione delle sottoscrizioni  
 Il server di report utilizza due tipi di eventi per attivare il processo di sottoscrizione, ovvero un evento basato sul tempo specificato in una pianificazione o un evento di aggiornamento di snapshot.  
  
 Un trigger basato sul tempo utilizza una pianificazione in base al report o una pianificazione condivisa per specificare quando deve essere eseguita una sottoscrizione. Per i report su richiesta e memorizzati nella cache le pianificazioni rappresentano la sola opzione di trigger.  
  
 Un evento di aggiornamento di snapshot utilizza l'aggiornamento pianificato di uno snapshot del report per attivare una sottoscrizione. È possibile definire una sottoscrizione che viene attivata quando il report viene aggiornato con nuovi dati in base alle proprietà di esecuzione impostate per il report.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una sottoscrizione guidata dai dati &#40;esercitazione su SSRS&#41;](../create-a-data-driven-subscription-ssrs-tutorial.md)   
 [Pianificazioni](schedules.md)   
 [Server di report di Reporting Services &#40;modalità nativa&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Creare e gestire sottoscrizioni per server di report in modalità nativa](../create-manage-subscriptions-native-mode-report-servers.md)   
 [Monitorare le sottoscrizioni di Reporting Services](monitor-reporting-services-subscriptions.md)  
  
  
