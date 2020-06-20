---
title: Creare una sessione eventi estesi utilizzando la finestra di dialogo nuova sessione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.SSMS.XEDISPLAY.GROUPING.F1
- SQL12.SSMS.XEDISPLAY.AGGREGATION.F1
- SQL12.SSMS.XEDISPLAY.NEWMERGEDCOLUMN.F1
- SQL12.SSMS.XENEWEVENTSESSION.GENERAL.F1
- SQL12.SSMS.XEDISPLAY.EDITCOLUMNS.F1
- SQL12.SSMS.XEDISPLAY.FILTERS.F1
helpviewer_keywords:
- Extended Events Dialog Box
ms.assetid: 6b2244bc-df6a-4b0a-990e-ddd8d42f7907
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 819aa4e09c30fc0b1c28373583f1e224899435d9
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84934518"
---
# <a name="create-an-extended-events-session-using-the-new-session-dialog"></a>Creare una sessione Eventi estesi utilizzando la finestra di dialogo Nuova sessione
  La finestra di dialogo Nuova sessione consente di definire una sessione di Eventi estesi che acquisisce, visualizza e analizza i dati. La finestra di dialogo Nuova sessione espone tutta la funzionalità di Eventi estesi.  
  
 La [Creazione guidata nuova sessione](../ssms/object/object-explorer.md) consente anche di definire una sessione di eventi estesi che supporta la maggior parte delle funzionalità degli eventi estesi.  
  
## <a name="before-you-begin"></a>Operazioni preliminari  
 Per aprire la finestra di dialogo Nuova sessione, in Esplora oggetti espandere il nodo **Gestione** , quindi espandere **Eventi estesi**. Fare clic con il pulsante destro del mouse su **Sessioni**, quindi scegliere **Nuova sessione**.  
  
##  <a name="permissions"></a><a name="BeforeYouBegin"></a> Autorizzazioni  
 Per creare una sessione Eventi estesi, è necessario disporre dell'autorizzazione ALTER ANY EVENT SESSION.  
  
## <a name="to-create-an-extended-events-session-using-the-new-session-dialog"></a>Per creare una sessione Eventi estesi utilizzando la finestra di dialogo Nuova sessione  
 Usare la pagina **Generale** per selezionare un modello e pianificare una sessione eventi.  
  
#### <a name="to-select-a-template-and-schedule-an-event-session"></a>Per selezionare un modello e pianificare una sessione eventi  
  
1.  In Esplora oggetti espandere il nodo **Gestione** , quindi espandere **Eventi estesi**. Fare clic con il pulsante destro del mouse su **Sessioni**, quindi scegliere **Nuova sessione**.  
  
2.  Nella casella **Nome sessione** della pagina **Generale** digitare un nome significativo per la sessione eventi.  
  
3.  Nella casella **Modello** selezionare il modello da usare nell'elenco a discesa.  
  
     È possibile selezionare uno dei modelli preconfigurati progettati per i problemi comuni oppure scegliere **Da file** per usare un file modello esportato da una definizione di sessione precedente. Si noti che è possibile modificare la configurazione della sessione anche dopo avere applicato il modello.  
  
4.  Per avviare la sessione quando si avvia il server, selezionare la casella di controllo **Avviare la sessione eventi all'avvio del server** nella sezione **Pianificazione** .  
  
     Per avviare la sessione dopo averla creata, selezionare la casella di controllo **Avviare la sessione eventi subito dopo la creazione della sessione** .  
  
5.  Per visualizzare i dati dinamici per la sessione eventi, fare clic su **Controllare i dati dinamici sullo schermo man mano che vengono acquisiti**. La traccia dei dati dinamici inizierà a essere visualizzata subito dopo la creazione della sessione.  
  
6.  Nella sezione **Rilevamento causalità** selezionare la casella di controllo **Tenere traccia della correlazione degli eventi** per tenere traccia del lavoro in più attività.  
  
     Per ulteriori informazioni sul rilevamento della causalità, vedere "contenuto e caratteristiche della sessione" nell'argomento [SQL Server di sessioni degli eventi estesi](../relational-databases/extended-events/sql-server-extended-events-sessions.md) .  
  
     Per aggiungere eventi alla sessione, fare clic su **Eventi** nella sezione **Selezione pagina**.  
  
    > [!NOTE]  
    >  Non fare clic su **OK** fino a quando non è stata completata la creazione della sessione eventi.  
  
 La pagina **Eventi** consente di trovare e aggiungere gli eventi da acquisire per la sessione.  
  
#### <a name="to-add-events-to-a-session"></a>Per aggiungere eventi a una sessione  
  
1.  Nella finestra di dialogo Nuova sessione selezionare **Eventi** nella sezione **Selezione pagina**.  
  
2.  Nella pagina **Eventi** fare clic su **Seleziona** (il pulsante **Seleziona** viene visualizzato in grigio se è già visualizzata la schermata **Selezionare gli eventi da acquisire** ).  
  
     È possibile cercare qualsiasi parola nella tabella immettendo il testo da cercare nella casella **Libreria di eventi** . Se, ad esempio, si vuole trovare l'evento **lock_acquired** , è possibile immettere **lock** o **lock acquire**.  
  
3.  Nella sezione **Libreria di eventi** selezionare il metodo da usare per la ricerca degli eventi da acquisire nell'elenco a discesa. È ad esempio possibile cercare i nomi di evento oppure i nomi di evento e le relative descrizioni. Immettere i criteri di ricerca nella casella **Cerca** .  
  
    > [!NOTE]  
    >  Gli eventi del canale **Debug** sono nascosti per impostazione predefinita. Per visualizzare gli eventi di debug, selezionare **Debug** dall'elenco a discesa **Canale** .  
  
     I dettagli relativi agli eventi selezionati vengono visualizzati nel riquadro Dettagli in **Libreria di eventi**.  
  
     Gli eventi sono elencati per nome, in ordine alfabetico. Per eseguire l'ordinamento in base ad altri dettagli dell'evento, fare clic sull'intestazione di colonna appropriata. È ad esempio possibile applicare un ordinamento in base alla colonna **Categoria** o **Canale** .  
  
4.  Selezionare l'evento o gli eventi da acquisire, quindi fare clic sulla freccia DESTRA per spostare gli eventi nella sezione **Eventi selezionati** .  
  
    > [!NOTE]  
    >  È possibile selezionare più eventi contemporaneamente in **Libreria di eventi** usando il tasto CTRL o MAIUSC.  
  
     Per configurare gli eventi selezionati, fare clic su **Configura**.  
  
    > [!NOTE]  
    >  Non fare clic su **OK** fino a quando non è stata completata la creazione della sessione eventi.  
  
 La pagina **Archivio dati** consente di aggiungere destinazioni a una sessione eventi. Le destinazioni consentono di archiviare i dati degli eventi ed eseguire azioni come il salvataggio di eventi in un file per la successiva visualizzazione e l'aggregazione dei dati degli eventi per la sessione. Per altre informazioni sulle destinazioni degli eventi estesi, vedere [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
 Di seguito sono illustrate le destinazioni che è possibile utilizzare per una sessione Eventi estesi:  
  
-   **etw_classic_sync_target**. Consente di correlare gli eventi di SQL Server con dati degli eventi dell'applicazione o del sistema operativo Windows.  
  
-   **event_counter**. Consente di contare tutti gli eventi specificati che si verificano dopo l'avvio di una sessione Eventi estesi. Consente di ottenere informazioni sulle funzionalità del carico di lavoro senza aggiungere l'overhead di un'intera raccolta di eventi.  
  
-   **event_file**. Consente di scrivere l'output della sessione eventi restituito dai buffer di memoria completi su disco.  
  
-   **histogram**. Consente di calcolare il numero di volte in cui si verifica un evento specificato, in base a un'azione o una colonna di evento specificata.  
  
-   **pair_matching**. Consente di determinare quando un evento associato specificato non si verifica in un set corrispondente.  
  
-   **ring_buffer**. Consente di mantenere i dati degli eventi in memoria secondo una modalità FIFO o secondo una modalità FIFO basata sul tipo di evento.  
  
#### <a name="to-configure-global-fields-for-a-session"></a>Per configurare campi globali per una sessione  
  
1.  Nella pagina **Eventi** fare clic su **Configura**dopo avere selezionato l'evento o gli eventi da aggiungere alla sessione eventi.  
  
     Dopo avere fatto clic su **Configura**, la sezione **Libreria di eventi** viene compressa e la sezione **Eventi selezionati** viene spostata verso la parte sinistra della pagina. La sezione **Opzioni di configurazione eventi** usata per configurare gli eventi viene visualizzata sul lato destro della pagina. Le schede di questa pagina consentono di configurare le azioni per la sessione eventi.  
  
2.  Nella scheda **Campi globali** selezionare i campi da applicare agli eventi selezionati.  
  
     È possibile selezionare più campi per ogni evento.  
  
    > [!NOTE]  
    >  Se per due eventi già selezionati sono configurate azioni diverse, tramite gli eventi estesi verranno visualizzate le azioni parzialmente selezionate. Per trovare rapidamente le azioni abilitate, è possibile applicare un ordinamento in base allo stato di abilitazione/disabilitazione facendo clic sull'intestazione di colonna sopra alle caselle di controllo.  
  
3.  La scheda  **Filtri** consente di applicare filtri (detti anche predicati) per limitare gli eventi da acquisire.  
  
     Se all'evento selezionato è applicato un filtro, nella colonna viene visualizzato un segno di spunta.  
  
    > [!NOTE]  
    >  È possibile selezionare più eventi a cui applicare un filtro utilizzando il tasto CTRL o MAIUSC. Verranno tuttavia visualizzati per la configurazione solo i campi evento comuni. Se per due eventi selezionati sono già configurati filtri diversi, il filtro non verrà visualizzato. Se i filtri vengono riconfigurati, i valori dei filtri esistenti vengono sovrascritti.  
  
    > [!NOTE]  
    >  Quando si configura una clausola group per il filtro, le parentesi ridondanti vengono rimosse dal filtro dopo che il risultato è stato salvato. Se, ad esempio, si crea un filtro che raggruppa **Clausola 1** e **Clausola 2**, le clausole vengono racchiuse tra parentesi. Dopo avere salvato il filtro, le parentesi ridondanti vengono rimosse. La rimozione delle parentesi non influisce sulla logica di filtro.  
  
4.  Nella scheda **Campi evento** selezionare i campi evento da applicare a un evento selezionato.  
  
     Gli eventi contengono diversi campi che vengono sempre raccolti e che sono visualizzati nella scheda **Campi evento** senza caselle di controllo. Un evento può disporre anche di campi facoltativi che non vengono raccolti per impostazione predefinita. I campi facoltativi con costo elevato non sono ad esempio selezionati. I campi facoltativi sono elencati anche nella scheda **Campi evento** con le caselle di controllo. Per raccogliere un campo facoltativo, selezionare la casella di controllo corrispondente.  
  
    > [!NOTE]  
    >  Nelle opzioni del campo evento verranno visualizzati i campi che saranno acquisiti e visualizzati nei risultati della traccia. Tramite gli eventi estesi vengono visualizzati solo i tipi di dati dei campi evento. I campi evento di sola lettura non vengono ad esempio visualizzati. Se si selezionano due o più eventi, nella finestra di dialogo Nuova sessione viene visualizzato uno spazio vuoto nella scheda **Campi evento** .  
  
5.  Per aggiungere destinazioni a una sessione eventi, selezionare **Archivio dati** nella sezione **Selezione pagina**.  
  
    > [!NOTE]  
    >  Non fare clic su **OK** fino a quando non è stata completata la creazione della sessione eventi.  
  
#### <a name="to-add-targets-to-an-event-session"></a>Per aggiungere destinazioni a una sessione eventi  
  
1.  Nella finestra di dialogo Nuova sessione selezionare **Archivio dati** nella sezione **Selezione pagina**.  
  
2.  Nella pagina **Archivio dati** selezionare il tipo di destinazione nell'elenco a discesa.  
  
     Dopo avere selezionato il tipo di destinazione, viene visualizzata la descrizione della destinazione. È possibile aggiungere una destinazione solo una volta. Se la destinazione è già stata aggiunta alla sessione, non verrà visualizzata nell'elenco a discesa.  
  
3.  Fare clic su **Aggiungi** per aggiungere una destinazione per la sessione eventi. Per rimuovere una destinazione, fare clic su **Rimuovi**.  
  
     Le proprietà della destinazione vengono visualizzate nella sezione **Destinazioni** , a seconda della destinazione selezionata.  
  
4.  Di seguito sono illustrate le proprietà che è possibile specificare, in base alla destinazione selezionata:  
  
    |Destinazione|Proprietà destinazione|  
    |------------|-----------------------|  
    |**etw_classic_sync_target**|**Nome del file di log sessione sul server**. Immettere il nome e la directory del file di log nel server oppure fare clic su **Sfoglia** per trovare e selezionare il file di log.<br /><br /> **Dimensioni massime file di log**. Immettere le dimensioni massime del file di log per l'evento ETW (Event Tracing for Windows, Analisi eventi per Windows). Il valore predefinito è 20 megabyte (MB). È possibile selezionare un'unità di archiviazione diversa nell'elenco a discesa.<br /><br /> **Dimensioni buffer**. Immettere le dimensioni del buffer in memoria per la sessione eventi. Il valore predefinito è 128 kilobyte (KB). È possibile selezionare un'unità di archiviazione diversa nell'elenco a discesa.<br /><br /> **Nome della sessione**. Immettere un nome di sessione ETW significativo.<br /><br /> **Riprova in caso di errore durante la scrittura di ETW**. Selezionare questa casella di controllo se si desidera che venga eseguito un nuovo tentativo di pubblicazione dell'evento nel sottosistema ETW.<br /><br /> **Numero massimo di tentativi**. Immettere il numero massimo di volte per cui si desidera che venga eseguito un nuovo tentativo di pubblicazione dell'evento nel sottosistema ETW prima di eliminare l'evento. Il numero di tentativi predefinito è zero (0). Per questa proprietà di destinazione, il valore zero (0) indica che non viene eseguito alcun tentativo.|  
    |**event_counter**|Non vi sono proprietà di destinazione per il contatore eventi.|  
    |**event_file**|**Nome file sul server**. Immettere la directory e il nome del file di destinazione nel server oppure fare clic su **Sfoglia** per trovare e selezionare il file di destinazione.<br /><br /> **Dimensioni massime del file**. Specificare le dimensioni massime del file per la destinazione file. Se non si specifica un valore massimo, le dimensioni del file aumenteranno fino a quando il disco non è pieno. Le dimensioni predefinite del file sono di 1 gigabyte (GB). È possibile selezionare un'unità di archiviazione diversa nell'elenco a discesa.<br /><br /> **Abilitare il rollover dei file**. Selezionare questa casella di controllo per abilitare il rollover dei file per la destinazione file.<br /><br /> **Numero massimo di file**. Immettere il numero massimo di file che si desidera mantenere nel file system.|  
    |**istogramma**|**Evento in base a cui filtrare**. Selezionare l'evento in base al quale si desidera applicare il filtro nell'elenco a discesa. È possibile applicare un filtro in base a qualsiasi evento incluso nella sessione eventi. È anche possibile selezionare **\<None>** dall'elenco a discesa per includere tutti gli eventi e i bucket di base sull'azione.<br /><br /> **Bucket di base in: Azione**. Selezionare questa opzione per basare i bucket sul nome dell'azione utilizzato come origine dati, quindi selezionare l'azione nell'elenco a discesa.<br /><br /> **Bucket di base in: Campo**. Selezionare questa opzione per basare i bucket sul campo evento utilizzato come origine dati, quindi selezionare il campo nell'elenco a discesa.<br /><br /> **Numero massimo di bucket**. Immettere il numero massimo di bucket che si desidera mantenere. Quando questo valore viene raggiunto, nella sessione eventi vengono ignorati i nuovi eventi che non appartengono ai bucket esistenti.|  
    |**pair_matching**|**Eventi: Inizia con**. Selezionare nell'elenco a discesa il nome di evento che specifica l'evento iniziale in una sequenza associata.<br /><br /> **Eventi: Termina con**. Selezionare nell'elenco a discesa il nome di evento che specifica l'evento finale in una sequenza associata.<br /><br /> **Campi e azioni: Inizia con**. Selezionare nell'elenco a discesa il campo e/o l'azione iniziale in una sequenza associata.<br /><br /> **Campi e azioni: Termina con**. Selezionare nell'elenco a discesa il campo e/o l'azione finale in una sequenza associata.<br /><br /> **Elimina nuovi eventi non associati in caso di memoria insufficiente**. Selezionare questa casella di controllo per interrompere la raccolta di eventi nella destinazione pair_matching quando vi è un utilizzo eccessivo della memoria del computer. La raccolta di eventi riprenderà non appena viene liberata memoria.<br /><br /> **Numero massimo di eventi orfani**. Specificare il numero massimo di eventi orfani che si desidera mantenere in memoria.|  
    |**ring_buffer**|**Numero di eventi da mantenere**. Utilizzare le frecce rivolte verso l'alto e verso il basso per specificare il numero di eventi che si desidera mantenere. Il valore predefinito è 1000.<br /><br /> **Dimensioni massime memoria buffer**. Immettere la quantità massima di memoria che può essere utilizzata. Quando questo valore viene raggiunto, gli eventi esistenti vengono eliminati. Il valore predefinito per le dimensioni della memoria è 0 megabyte (MB), che indica dimensioni illimitate. È possibile selezionare un'unità di archiviazione diversa nell'elenco a discesa.<br /><br /> **Mantenere un numero specificato di eventi (per tipo) quando il buffer è pieno**. Selezionare questa opzione per mantenere il numero specificato di eventi di ogni tipo nel buffer.<br /><br /> **Numero di eventi da mantenere (per tipo)**. Immettere il numero desiderato di eventi di ogni tipo da mantenere nel buffer.|  
  
5.  Per impostare le proprietà di configurazione avanzate, selezionare **Avanzate** nella sezione **Selezione pagina** .  
  
    > [!NOTE]  
    >  Non fare clic su **OK** fino a quando non è stata completata la creazione della sessione eventi.  
  
#### <a name="to-set-advanced-configurations"></a>Per impostare le opzioni di configurazione avanzate.  
  
1.  Nella finestra di dialogo Nuova sessione selezionare **Avanzate** nella sezione **Selezione pagina**.  
  
2.  Nella pagina **Avanzate** specificare le opzioni **Modalità memorizzazione eventi** per la sessione eventi con le operazioni seguenti:  
  
    1.  **Perdita di singoli eventi**. Selezionare questa opzione per consentire la perdita di un singolo evento.  
  
    2.  **Perdita di più eventi**. Selezionare questa opzione per consentire la perdita di più eventi.  
  
    3.  **Perdita di nessun evento**. Selezionare questa opzione se si desidera impedire la perdita di eventi. Questa opzione non è consigliata.  
  
        > [!NOTE]  
        >  Alcuni eventi, ad esempio l'evento **sqlos.wait_info** , non sono compatibili con la modalità di memorizzazione **Perdita di nessun evento** .  
  
3.  Per specificare le opzioni di **Latenza di recapito massima** per la sessione eventi, procedere come segue:  
  
    1.  **In secondi**. Selezionare questa opzione per prolungare o abbreviare la latenza di recapito massima. Utilizzare le frecce rivolte verso l'alto e verso il basso per specificare la latenza di recapito massima in secondi.  
  
    2.  **Senza limiti**. Selezionare questa opzione se si desidera che gli eventi vengano recapitati solo quando il buffer è pieno.  
  
4.  Nella casella **Dimensioni memoria massime** immettere le dimensioni massime della memoria. Quando questo valore viene raggiunto, gli eventi esistenti vengono eliminati. È possibile selezionare un'unità di archiviazione diversa nell'elenco a discesa.  
  
5.  Nella casella **Dimensioni eventi massime** immettere le dimensioni massime per gli eventi troppo grandi per essere contenuti in **Dimensioni memoria massime**. Se non si raccolgono eventi di dimensioni molto grandi, non è necessario configurare questa opzione. È possibile selezionare un'unità di archiviazione diversa nell'elenco a discesa.  
  
6.  Per specificare le opzioni di **Modalità partizione di memoria** per la sessione eventi, procedere come segue:  
  
    1.  **Nessuno**. Selezionare questa opzione se non si desidera una modalità di partizione di memoria.  
  
    2.  **Per nodo**. Selezionare questa opzione se si desidera partizionare la memoria per nodo.  
  
    3.  **Per CPU**. Selezionare questa opzione se si desidera partizionare la memoria per CPU.  
  
 Per ripristinare i valori predefiniti della configurazione per le proprietà della sessione precedente, fare clic su **Ripristina impostazioni predefinite**.  
  
## <a name="see-also"></a>Vedere anche  
 [Creare una sessione eventi estesi tramite l'editor di query](../../2014/database-engine/create-an-extended-events-session-using-query-editor.md)   
 [Creare una sessione eventi estesi utilizzando la procedura guidata &#40;Esplora oggetti&#41;](../ssms/object/object-explorer.md)   
 [Creare uno script per una sessione Eventi estesi](../../2014/database-engine/script-an-extended-event-session.md)  
  
  
