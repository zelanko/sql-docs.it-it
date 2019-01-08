---
title: Configurare Usage Data Collection for (Power Pivot per SharePoint | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 52a2754a4c6410430042f2b31805db42def4ec1f
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52420282"
---
# <a name="configure-usage-data-collection-for-power-pivot-for-sharepoint"></a>Configurare la raccolta dati di utilizzo per PowerPivot per SharePoint
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  La raccolta dati di utilizzo è una funzionalità di SharePoint a livello di farm. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint questo sistema viene usato ed esteso per fornire i report nel dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in cui viene mostrato l'uso dei servizi e dei dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . A seconda dell'installazione di SharePoint, la raccolta dati di utilizzo potrebbe essere disabilitata per la farm. È necessario che un amministratore della farm abiliti la registrazione dell'utilizzo per creare i dati di utilizzo che vengono visualizzati nel dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Per informazioni sui dati di utilizzo nel dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , vedere [Dati di utilizzo e dashboard di gestione PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
 **Contenuto dell'argomento:**  
  
 [Abilitare la raccolta dati di utilizzo e scegliere eventi che attivino la raccolta dati](#events)  
  
 [Impostare il percorso del file di log](#configdb)  
  
 [Configurare i processi timer utilizzati nella raccolta dati di utilizzo](#jobs)  
  
 [Definire la durata del periodo di archiviazione della cronologia dei dati sull'utilizzo](#confighist)  
  
 [Definire le categorie delle risposte alle query veloce, media e lenta per la creazione di report](#qrh)  
  
 [Specificare la frequenza con la quale le statistiche di query vengono segnalate nel sistema di raccolta dei dati di utilizzo](#ttr)  
  
 [Aprire la pagina dell'applicazione del servizio PowerPivot per accedere alle impostazioni di configurazione](#openconfig)  
  
 [Configurazione predefinita per la raccolta dati di utilizzo di PowerPivot](#defaultconfig)  
  
> [!IMPORTANT]  
>  I dati sull'utilizzo forniscono indicazioni sulle modalità con cui gli utenti accedono a dati e risorse, ma non garantiscono dati affidabili e persistenti sulle operazioni server e l'accesso utente. Nel caso di un riavvio del server, ad esempio, i dati sull'utilizzo dell'evento andranno persi in modo irreversibile. Analogamente, se i file di log temporanei raggiungono le dimensioni massime stabilite, non verranno aggiunti altri dati finché il contenuto dei file non verrà cancellato. Se è necessario disporre di una funzione di controllo, considerare la possibilità di utilizzare le funzionalità del flusso di lavoro e del tipo di contenuto di SharePoint che offrono un sottosistema di controllo per la farm. Per ulteriori informazioni, cercare la documentazione relativa al prodotto e alla community sul Web.  
  
##  <a name="events"></a> Abilitare la raccolta dati di utilizzo e scegliere eventi che attivino la raccolta dati  
 Configurare la raccolta dati di utilizzo in Amministrazione centrale SharePoint.  
  
1.  In Amministrazione centrale fare clic su **Monitoraggio**.  
  
2.  Nella sezione **Report**fare clic su **Configura raccolta dati di utilizzo e integrità**.  
  
3.  Selezionare **Abilita raccolta dati di utilizzo**.  
  
4.  Nella sezione **Eventi da registrare** selezionare o deselezionare le caselle di controllo per abilitare o disabilitare gli eventi di Analysis Services seguenti:  
  
    |Evento|Descrizione|  
    |-----------|-----------------|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Connessioni**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene usato per monitorare le connessioni al server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] effettuate per conto di un utente.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] - Utilizzo dati di caricamento**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene usato per monitorare le richieste per il caricamento dei dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] nella memoria del server. Un evento di caricamento viene generato per i file di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] caricati da un database del contenuto o dalla cache.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] - Utilizzo dati di scaricamento**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene usato per monitorare le richieste per lo scaricamento di un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] dopo un periodo di inattività. La memorizzazione nella cache su disco di un'origine dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] verrà segnalata come un evento di scaricamento.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] - Utilizzo query**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] viene usato per monitorare i tempi di elaborazione query dei dati caricati in un'istanza di [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] .|  
  
    > [!NOTE]  
    >  Anche le operazioni di aggiornamento dati e prevenzione e risoluzione dei problemi del server generano dati sull'utilizzo, ma a questi processi non è associato alcun evento.  
  
5.  Inoltre, è possibile aggiornare il percorso del file di log. Per ulteriori informazioni, vedere la sezione successiva.  
  
6.  Scegliere **OK** per salvare le modifiche.  
  
7.  Facoltativamente, è possibile specificare se registrare tutti i messaggi o solo gli errori. Per altre informazioni su come limitare i messaggi di evento, vedere [Configurare e visualizzare i file di log di SharePoint e la registrazione diagnostica &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
##  <a name="configdb"></a> Impostare il percorso del file di log  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono inizialmente archiviati nei file di log dei dati di utilizzo nel server locale e, successivamente, spostati a intervalli regolari nel database dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Il percorso del file di log viene impostato in Amministrazione centrale. Il percorso predefinito è:  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 Per visualizzare o modificare queste proprietà, utilizzare la pagina **Raccolta dati di utilizzo e integrità** .  
  
1.  Nella home page di Amministrazione centrale fare clic su **Monitoraggio**.  
  
2.  Nella sezione Monitoraggio fare clic su **Configura raccolta dati su utilizzo e integrità**.  
  
3.  Nelle impostazioni della raccolta dati di utilizzo visualizzare o modificare il percorso, il nome o le dimensioni massime del file. Se si specificano dimensioni troppo basse, il file raggiungerà rapidamente il limite e non verranno aggiunte nuove voci finché il contenuto non verrà spostato nel database di raccolta dei dati sull'utilizzo centrale.  
  
##  <a name="jobs"></a> Configurare i processi timer utilizzati nella raccolta dati di utilizzo  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] vengono spostati in percorsi diversi nel sistema di raccolta dati di utilizzo tramite due processi timer:  
  
-   Il processo timer di "Microsoft SharePoint Foundation importazione dati di utilizzo" Sposta [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] tra l'utilizzo del [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] database dell'applicazione di servizio.  
  
-   Il "[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] processo timer di elaborazione Dashboard di gestione" i dati da [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] della cartella di lavoro che rappresenta l'origine dei dati per report amministrativi predefiniti.  
  
 Se è necessario aggiornare i report amministrativi visualizzati più frequentemente nel dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , seguire questa procedura.  
  
1.  In Amministrazione centrale fare clic su **Monitoraggio**.  
  
2.  Scegliere **Rivedi definizioni processi** Nella sezione **Processi timer** .  
  
3.  Fare clic su **Importazione dati di utilizzo di Microsoft SharePoint Foundation**.  
  
4.  Fare clic su **Esegui**. Se il pulsante **Esegui ora** è disabilitato fare clic su **Abilita** , quindi selezionare **Esegui ora**.  
  
5.  Nell'elenco Definizioni processi fare clic su **Processo timer di elaborazione dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
6.  Fare clic su **Esegui**.  
  
7.  Selezionare i report per visualizzare i dati di aggiornamento. Per altre informazioni, vedere [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="confighist"></a> Definire la durata del periodo di archiviazione della cronologia dei dati sull'utilizzo  
 La cronologia dei dati sull'utilizzo viene archiviata per eventi (connessioni, caricamenti, scaricamenti ed elaborazione query su richiesta) e per l'aggiornamento dei dati (elaborazione pianificata dei dati). Sebbene i dati di utilizzo vengano raccolti attraverso il sistema di raccolta dei dati di utilizzo di SharePoint, verranno in seguito spostati in un database dell'applicazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e in un database Reporting per un'archiviazione a lungo termine. L'impostazione della cronologia dei dati di utilizzo specifica per quanto tempo i dati di utilizzo verranno mantenuti nei database dell'applicazione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Lo stesso limite si applica in modo analogo a tutti i tipi di dati di utilizzo archiviati nello stesso database dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
1.  [Aprire la pagina dell'applicazione del servizio PowerPivot](#openconfig).  
  
2.  Nella sezione **Raccolta dati di utilizzo** in **Cronologia dati di utilizzo**specificare per quanti giorni si desidera mantenere un record dell'attività di aggiornamento dati per ogni cartella di lavoro.  
  
    -   Il valore predefinito è 365 giorni.  
  
    -   0 specifica un'archiviazione senza limiti di tempo, ovvero i dati vengono conservati all'infinito.  
  
    -   In alternativa, è possibile specificare un intervallo compreso tra 1 e 5000.  
  
     Se si limita il periodo di memorizzazione a un numero inferiore di giorni, tutti i dati che superano il nuovo limite verranno eliminati. Ad esempio, se si modifica il valore da 365 a 30, verranno eliminate tutte le informazioni cronologiche risalenti a più di 30 giorni prima. Verranno mantenuti solo i dati degli ultimi 30 giorni.  
  
     I dati verranno effettivamente eliminati al verificarsi dell'evento successivo. Il limite sulla cronologia dei dati sull'utilizzo viene controllato solo quando il sistema elabora un evento.  
  
3.  Fare clic su **OK**.  
  
 Per altre informazioni sulla raccolta e sull'archiviazione dei dati di utilizzo, vedere [Raccolta dati di utilizzo di PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="qrh"></a> Definire le categorie delle risposte alle query veloce, media e lenta per la creazione di report  
 Le prestazioni di elaborazione query vengono misurate rispetto a categorie predefinite che definiscono un ciclo di risposta alle richieste in base al tempo necessario per il completamento. Le categorie predefinite includono: Semplice, rapida, prevista, con esecuzione prolungata e superata. Ogni richiesta a un server [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] rientrerà in una di queste categorie in base al tempo necessario per il completamento.  
  
 Le informazioni sulle risposte alle query vengono utilizzate nei report di attività. All'interno dei report, ogni categoria viene usata in modo diverso per rivelare nel modo migliore le tendenze delle prestazioni del sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Ad esempio, le richieste semplici vengono escluse completamente per mostrare unicamente le tendenze più significative attraverso le categorie rimanenti. Le statistiche sulle richieste con esecuzione prolungata o superate sono invece molto presenti nei report per dare la possibilità agli amministratori o ai proprietari della cartella di lavoro di intraprendere immediatamente azioni correttive.  
  
 Sebbene non sia possibile aggiungere o eliminare categorie, è possibile definire i limiti superiori e inferiori che determinano la fine di una categoria e l'inizio di un'altra. Se l'organizzazione utilizza contratti sui livelli di servizio (SLA) per definire livelli accettabili di prestazioni e disponibilità dei server, è possibile ottimizzare queste categorie in base al contratto creato.  
  
1.  [Aprire la pagina dell'applicazione del servizio PowerPivot](#openconfig).  
  
2.  Nella sezione **Raccolta dati di utilizzo** , in **Limite massimo risposta semplice** , immettere un valore (in millisecondi) per impostare il limite massimo per il completamento di una risposta semplice. Le richieste che rientrano in questa categoria includono in genere ping del server, inizializzazioni di sessioni e query di metadati. L'impostazione predefinita è 500 millisecondi (o mezzo secondo).  
  
3.  In Limite massimo risposta rapida immettere un valore (in millisecondi) per impostare il limite massimo per il completamento di una risposta rapida. Le richieste che rientrano in questa categoria includono le query di set di dati molto piccoli o di server dei metadati di set di dati di grandi dimensioni. L'impostazione predefinita è 1000 millisecondi (o un secondo).  
  
4.  In **Limite massimo risposta prevista**immettere un valore (in millisecondi) per impostare il limite massimo per il completamento di una risposta in un periodo di tempo medio o previsto. Le richieste che rientrano in questa categoria includono il caricamento di dati in un visualizzatore. L'impostazione predefinita è 3000 millisecondi (o 3 secondi).  
  
5.  In **Limite massimo risposta lunga**immettere un valore (in millisecondi) per impostare il limite massimo per il completamento di una risposta con esecuzione prolungata. Le richieste che rientrano in questa categoria richiedono un'esecuzione più lunga, ma in un intervallo di tempo comunque accettabile. L'impostazione predefinita è 10000 millisecondi (o 10 secondi).  
  
     Le richieste che superano questo limite rientrano nella categoria *Superato*. Non è prevista alcuna soglia configurabile per *Superato*. Deriva dal limite superiore specificato in Limite massimo risposta lunga. Le richieste che rientrano nella categoria Superato hanno un'esecuzione più lunga di quanto non sia consentito dallo SLA definito.  
  
6.  Fare clic su **OK**.  
  
##  <a name="ttr"></a> Specificare la frequenza con la quale le statistiche di query vengono segnalate nel sistema di raccolta dei dati di utilizzo  
 L'intervallo tempo-segnalazione specifica la frequenza con la quale le statistiche di query vengono segnalate nel sistema di raccolta dei dati sull'utilizzo. Le statistiche sulle query si accumulano in un processo e vengono riportate come un singolo evento a intervalli regolari. È possibile regolare l'intervallo per scrivere nel file di log con maggiore o minore frequenza.  
  
1.  [Aprire la pagina dell'applicazione del servizio PowerPivot](#openconfig).  
  
2.  Nella sezione **Raccolta dati di utilizzo** , in **Intervallo di report query**, immettere il numero di secondi dopo i quali le statistiche sulle query di tutte le categorie (semplice, rapida, prevista, esecuzione prolungata e superata) verranno segnalate dal server come singolo evento nel sistema di raccolta dati di utilizzo.  
  
    -   L'intervallo è compreso tra 1 e qualsiasi numero intero positivo.  
  
    -   L'impostazione predefinita è 300 secondi (o 5 minuti). Questo valore è consigliato per gli ambienti farm dinamici in cui viene eseguita una varietà di applicazioni e servizi.  
  
     Se questo valore viene aumentato in modo considerevole, è possibile che alcuni dati statistici vadano persi prima di essere registrati. Il riavvio di un servizio, ad esempio, causa la perdita delle statistiche relative alle query. Viceversa, se i report di attività predefiniti contengono dati insufficienti, considerare la possibilità di ridurre l'intervallo per ottenere più frequentemente eventi tempo-segnalazione.  
  
3.  Fare clic su **OK**.  
  
##  <a name="openconfig"></a> Aprire la pagina dell'applicazione del servizio PowerPivot per accedere alle impostazioni di configurazione  
 Solo gli amministratori di un servizio o di una farm possono modificare le impostazioni dell'applicazione di servizio. Se nella farm sono state definite più applicazioni del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , è necessario modificare ognuna singolarmente.  
  
1.  In **Gestione applicazioni**di Amministrazione centrale SharePoint fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Trovare l'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . È possibile identificare un'applicazione di servizio in base al tipo. Un tipo di applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] è **Applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
3.  Fare clic sul nome dell'applicazione del servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Verrà aperto il dashboard di gestione [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
4.  In **Azioni**fare clic su **Configura impostazioni dell'applicazione di servizio**. Verrà visualizzata la pagina Impostazioni applicazioni del servizio di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
##  <a name="defaultconfig"></a> Configurazione predefinita per la raccolta dati di utilizzo di PowerPivot  
 La raccolta dei dati di utilizzo per le operazioni di servizio [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] può essere abilitata con le impostazioni predefinite per renderla immediatamente disponibile nelle applicazioni che supportano la funzionalità di integrazione di Analysis Services. Le impostazioni predefinite includono eventi che attivano la raccolta dei dati sull'utilizzo, limiti sulla durata del periodo di archiviazione e soglie che suddividono in categorie i tempi di risposta query.  
  
 Nella tabella seguente sono riportati i valori predefiniti per la configurazione della raccolta dei dati sull'utilizzo.  
  
|Impostazione|Valore predefinito|Tipo|Intervallo valido|  
|-------------|-------------------|----------|-----------------|  
|**Eventi di uso di Analysis Services** (Connessione, Caricamento, Scaricamento, Richieste)|\<abilitato >|Boolean|Questi valori sono abilitati o disabilitati.|  
|**Query Reporting interval**|300 (in secondi)|Integer|Tra 1 e qualsiasi numero intero positivo. Il valore predefinito è 5 minuti.|  
|**Usage data history**|365 (in giorni)|Integer|0 specifica nessun limite, ma è anche possibile impostare un limite massimo per imporre una scadenza sui dati cronologici e l'eliminazione automatica. I valori validi per un periodo di memorizzazione limitato sono compresi tra 1 e 5000 (in giorni).|  
|Limite massimo risposta semplice|500 (in millisecondi)|Integer|Imposta un limite massimo che definisce uno scambio richiesta-risposta semplice. Qualsiasi richiesta completata entro un intervallo di tempo compreso tra 0 e 500 millisecondi viene considerata una richiesta semplice e ignorata ai fini del report.|  
|Limite massimo risposta rapida|1000 (in millisecondi)|Integer|Imposta un limite massimo che definisce uno scambio richiesta-risposta rapido.|  
|Limite massimo risposta prevista|3000 (in millisecondi)|Integer|Imposta un limite massimo che definisce uno scambio richiesta-risposta previsto.|  
|Limite massimo risposta con esecuzione prolungata|10000 (in millisecondi)|Integer|Imposta un limite massimo che definisce uno scambio richiesta-risposta con esecuzione prolungata. Tutte le richieste che superano questo limite massimo rientrano nella categoria Superato, che non prevede una soglia massima.|  
  
## <a name="see-also"></a>Vedere anche  
 [Documentazione di riferimento per le impostazioni di configurazione &#40;Power Pivot per SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Raccolta dati di utilizzo di PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
  
