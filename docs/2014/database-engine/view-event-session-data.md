---
title: Visualizzare i dati della sessione eventi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: ac742a01-2a95-42c7-b65e-ad565020dc49
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e2fecf8a71854d7f8df160ba3ff63912086a34e5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67131796"
---
# <a name="view-event-session-data"></a>Visualizzare i dati della sessione eventi
  In questo argomento verrà descritto l'utilizzo dell'interfaccia utente visualizzata per vedere e analizzare i dati degli eventi estesi:  
  
-   Visualizza dati di destinazione  
  
-   Utilizzo dei dati  
  
## <a name="view-target-data"></a>Visualizza dati di destinazione  
 È possibile visualizzare i dati raccolti nella destinazione specificata in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="view-target-data"></a>Visualizza dati di destinazione  
 Per visualizzare i dati di destinazione:  
  
1.  In Esplora oggetti espandere **Gestione**, **Eventi estesi**, **Sessioni**, quindi espandere una sessione.  
  
2.  Fare clic con il pulsante destro del mouse sul nome della destinazione, quindi scegliere **Visualizza dati di destinazione** per visualizzare i dati di destinazione.  
  
     Nella vista predefinita della finestra dei dati di destinazione vengono visualizzati i dati di destinazione.  
  
 Note sulla visualizzazione dei dati di destinazione:  
  
-   I dati di destinazione non sono disponibili per la destinazione ETW.  
  
-   Per visualizzare i dati ring_buffer in formato xml, nella finestra dei dati di destinazione fare clic sul collegamento **dati di destinazione ring_buffer** . Il file ring_buffer.xml viene visualizzato nell'editor XML.  
  
-   Per una destinazione event_file, visualizzare i dati di destinazione del file (file XEL) utilizzando uno dei metodi seguenti:  
  
    -   Usare file > Apri in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].
    
    -   Trascinare e rilasciare il file in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. 
    
    -   Fare doppio clic sul file XEL.  
    
    -   In [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]fare clic con il pulsante destro del mouse su una sessione Eventi estesi in esecuzione e selezionare Visualizza dati di destinazione. 
    
    -   [fn_xe_file_target_read_file](/sql/relational-databases/system-functions/sys-fn-xe-file-target-read-file-transact-sql).
    
    -   Usare PowerShell Read-SQLXevent nel [modulo SqlServer. XEvent](https://www.powershellgallery.com/packages/SqlServer.XEvent).
    
    -   Utilizzare XEvent a livello di codice utilizzando [XELite NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.XEvent.XELite).
    
    -   È possibile visualizzarne più di uno. File XEL selezionando **Unisci file di eventi estesi** dal menu apri file >.

### <a name="watching-live-data"></a>Controllo dei dati dinamici  
 È possibile controllare i dati dinamici mentre vengono acquisiti.  
  
-   In Esplora oggetti espandere i nodi **Gestione**, **Eventi estesi**, quindi **Sessioni** .  

-   Fare clic con il pulsante destro del mouse sul nome della sessione, quindi scegliere **Controlla i dati dinamici** per avviare la visualizzazione dei dati di traccia.  
  
     Le colonne che vengono visualizzate per impostazione predefinita sono **Nome evento** e **Timestamp**.  
  
     Per aggiungere colonne aggiuntive alla finestra della traccia, fare clic sul pulsante **Scegli colonne** sulla barra degli strumenti Eventi estesi. Nella scheda **Dettagli** verranno visualizzati tutti i dettagli dell'evento selezionato.  
  
     Gli eventi vengono in genere visualizzati in 30 secondi. Se si desidera modificare il periodo di latenza, è possibile modificare il valore di **Latenza di recapito massima** nella pagina **Avanzate** della finestra di dialogo **Nuova sessione** .  
     
-    I dati dinamici possono essere trasmessi tramite il [modulo PowerShell SqlServer. XEvent](https://www.powershellgallery.com/packages/SqlServer.XEvent).
     
### <a name="to-refresh-target-data"></a>Per aggiornare i dati di destinazione  
 L'aggiornamento dei dati di destinazione non è supportato per le destinazioni event_file:  
  
1.  Per aggiornare automaticamente i dati di destinazione, fare clic con il pulsante destro del mouse sui dati di destinazione, selezionare **Intervallo di aggiornamento**, quindi selezionare l'intervallo di aggiornamento dal relativo elenco.  
  
2.  Per sospendere e riprendere l'aggiornamento automatico, fare clic con il pulsante destro del mouse sui dati di destinazione e selezionare **Sospendi** o **Riprendi**.  
  
3.  Per aggiornare manualmente i dati di destinazione, fare clic con il pulsante destro del mouse sui dati di destinazione, quindi selezionare **Aggiorna**.  
  
## <a name="working-with-data"></a>Utilizzo dei dati  
 È possibile utilizzare le funzionalità di analisi dell'interfaccia utente degli eventi estesi per identificare i problemi.  
  
### <a name="details-pane"></a>Riquadro Dettagli  
 Nel riquadro **Dettagli** vengono visualizzate tutte le colonne per l'evento selezionato, inclusi campi e azioni. È possibile aggiungere una colonna alla tabella dei dati di destinazione facendo clic con il pulsante destro del mouse su una riga nel riquadro **Dettagli** e selezionando **Mostra colonna in tabella**.  
  
### <a name="create-modify-or-delete-merged-columns"></a>Creare, modificare o eliminare le colonne unite  
 Con una colonna unita è possibile combinare un set di campi da visualizzare in una sola colonna. Nella colonna unita verranno mostrati i dati dal primo campo non Null in base all'ordine con cui vengono aggiunti all'elenco dei campi. Si tratta di una situazione simile a quella visualizzata in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Profiler, dove in una colonna specifica è possibile visualizzare dati diversi a seconda dell'evento. Il relativo esempio più comune è il campo TextData in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Profiler. Per un esempio, è possibile unire i campi statement e batch_text rispettivamente dagli eventi sql_statement_completed e sql_batch_completed in un campo denominato myStatement. Quando si visualizza la colonna myStatement nella tabella, in essa verranno mostrati i dati appropriati per l'evento associato.  
  
 È possibile creare, modificare o eliminare le colonne unite:  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione e scegliere **Controlla i dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia fare clic con il pulsante destro del mouse sull'intestazione di colonna, quindi fare clic su **Scegli colonne**.  
  
 Per creare una colonna unita, fare clic su **Nuova** nella finestra di dialogo **Scegli colonne** .  Nella finestra di dialogo **Nuova colonna unita** assegnare un nome alla colonna unita e selezionare le colonne originali da includere nella colonna in questione.  
  
 Per modificare una colonna unita, selezionarne una nella finestra di dialogo **Scegli colonne** e fare clic su **Modifica**. Nella finestra di dialogo **Modifica colonna unita** rinominare la colonna unita o modificare le colonne originali da includere nella colonna unita.  
  
 Per eliminare una colonna unita, selezionarne una nella finestra di dialogo **Scegli colonne** e fare clic su **Elimina**.  
  
### <a name="filter-results"></a>Filtrare i risultati  
 È possibile visualizzare i risultati della traccia e, successivamente, applicare dei filtri per limitarne la visualizzazione nella finestra di traccia. Nel filtro di visualizzazione sono inclusi un filtro temporale e un filtro avanzato. È possibile utilizzare il filtro temporale per filtrare i risultati della traccia in base al timestamp dell'evento e il filtro avanzato per costruire condizioni di filtro utilizzando i campi e le azioni dell'evento. Esiste una relazione "and" tra i filtri temporale e avanzato.  
  
 Per creare un filtro:  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione e scegliere **Controlla i dati dinamici**.  
  
2.  Nella finestra dei risultati della traccia selezionare i risultati che si desidera filtrare, quindi nella barra degli strumenti **Eventi estesi** fare clic su **Filtri**.  
  
3.  Nella finestra di dialogo **Filtri** selezionare **Imposta filtro temporale** per impostare questo tipo di filtro trascinando le barre del dispositivo di scorrimento o modificando il tempo nella casella di modifica.  
  
4.  Nella sezione **Filtri aggiuntivi** applicare i criteri di filtro, quindi fare clic su **Applica**.  
  
### <a name="sort-results"></a>Ordinare i risultati  
 Per ordinare i risultati in ordine crescente o decrescente:  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sul pulsante **Arresta feed di dati** sulla barra degli strumenti.  
  
2.  Nella finestra dei risultati della traccia fare clic con il pulsante destro del mouse sull'intestazione di colonna che si desidera ordinare e scegliere **Ordinamento crescente** oppure **Ordinamento decrescente**.  
  
 È inoltre possibile fare clic sull'intestazione di colonna per invertire l'ordinamento.  
  
 In caso di raggruppamento di colonne, il relativo ordinamento comporta l'esecuzione della stessa operazione esclusivamente per i dati all'interno del gruppo.  
  
### <a name="group-results"></a>Raggruppare i risultati  
 La funzionalità dei risultati raggruppati è simile a quella della clausola `GROUP BY` in [!INCLUDE[tsql](../includes/tsql-md.md)]. Nella tabella dei dati di destinazione verranno mostrati i dati raggruppati, consentendo all'utente di espandere e comprimere i dati.  
  
 È necessario raggruppare i dati prima di poter aggregarli. Ad esempio, è possibile raggruppare in base al valore query_hash, disporre in ordine decrescente in base alla durata, ottenere la durata media per ogni gruppo, quindi disporre in modo decrescente in base all'aggregazione.  In questo modo verrà generato un elenco contenente istruzioni univoche dalla durata media più lunga a quella più corta. Quando si espande il gruppo di livello superiore verranno visualizzate le singole esecuzioni della query specificata, ordinate dalla più lunga alla più corta.  
  
 È possibile raggruppare i risultati per singola colonna o per più colonne.  
  
 Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sul pulsante **Arresta feed di dati** sulla barra degli strumenti.  
  
 Per raggruppare i risultati per singola colonna, fare clic con il pulsante destro del mouse sull'intestazione di colonna nella finestra dei risultati della traccia, quindi scegliere **Raggruppa per questa colonna**. Per annullare il raggruppamento, selezionare una delle righe e fare clic su **Rimuovi tutti i raggruppamenti**.  
  
 Per raggruppare i risultati per più colonne, fare clic sul pulsante **Raggruppamento** nella barra degli strumenti **Eventi estesi** . Nella casella **Colonne disponibili** della finestra di dialogo **Raggruppamento** selezionare le colonne da raggruppare e spostarle nella casella **Colonne raggruppate per** . Per modificare l'ordine nella casella **Colonne raggruppate per** fare clic sulle frecce SU o GIÙ.  
  
### <a name="aggregate-results"></a>Aggregare i risultati  
 È possibile visualizzare i risultati della traccia, quindi analizzare ulteriormente i dati evento aggregando colonne nei risultati. Eventi estesi supporta cinque funzioni di aggregazione:  
  
-   Sum  
  
-   Min  
  
-   max  
  
-   average  
  
-   count  
  
 Sum, min, max e average possono essere utilizzate solo con colonne numeriche. Count è il numero di valori non Null esistente per la colonna selezionata nel gruppo.  
  
 L'aggregazione viene eseguita in un gruppo, pertanto è necessario raggruppare i risultati prima di effettuare l'aggregazione. Per aggregare i risultati:  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione, selezionare **Controlla dati dinamici**, quindi fare clic sul pulsante **Arresta feed di dati** sulla barra degli strumenti.  
  
2.  Nella barra degli strumenti **Eventi estesi** fare clic sul pulsante **Aggregazione** . Nella finestra di dialogo Aggregazione verranno visualizzate le colonne disponibili per l'aggregazione.  
  
3.  Nella colonna **Tipo di aggregazione** selezionare il tipo di aggregazione.  
  
4.  Nella casella **Ordina aggregazione per** selezionare la colonna di ordinamento. Successivamente, selezionare l'ordinamento crescente o decrescente.  
  
### <a name="search-for-text-in-columns"></a>Cercare un testo nelle colonne  
 È possibile cercare un testo nelle colonne effettuando i passaggi seguenti:  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione e scegliere **Controlla i dati dinamici**.  
  
2.  Fare clic su **Trova** nella barra degli strumenti **Eventi estesi** .  
  
3.  Nella casella **Trova** della finestra di dialogo **Trova in eventi estesi** immettere il testo di ricerca. È possibile selezionare una delle ultime 20 stringhe di ricerca nell'elenco a discesa.  
  
4.  Nella casella **Cerca in** selezionare il percorso per cercare il testo specificato. Per la ricerca, utilizzare le opzioni seguenti:  
  
    -   Colonne della tabella. Utilizzare questa opzione per eseguire ricerche in tutte le colonne visibili nella finestra di traccia.  
  
    -   Dettagli. Utilizzare questa opzione per eseguire la ricerca in tutte le colonne (promosse e non promosse) della finestra di traccia selezionate prima di aprire la finestra **di dialogo trova in eventi estesi** .  
  
    -   *Event_column_name*. Utilizzare questa opzione per eseguire ricerche in una colonna specifica dell'evento dall'elenco a discesa.  
  
5.  Utilizzare le opzioni seguenti per specificare la modalità con cui si desidera definire la ricerca:  
  
    -   Maiuscole/minuscole. Utilizzare questa opzione per visualizzare i risultati della ricerca del testo immesso nella casella Trova corrispondenti sia in termini di contenuto sia in termini di applicazione della distinzione tra maiuscole e minuscole.  
  
    -   Parola intera. Utilizzare questa opzione per visualizzare solo i risultati della ricerca del testo immesso che corrispondono a parole intere.  
  
    -   Cerca in alto. Utilizzare questa opzione per eseguire la ricerca dalla posizione del cursore fino all'inizio dei risultati.  
  
    -   Usa. Utilizzare questa opzione per interpretare le espressioni regolari e i caratteri speciali immessi nella casella Trova. Tra i caratteri speciali sono inclusi i caratteri jolly (*) e (?) per rappresentare uno o più caratteri. Le espressioni regolari sono notazioni speciali utilizzate per definire i criteri del testo di ricerca.  
  
    -   Fare clic su **Trova successivo** per cercare il successivo testo immesso nella casella **Trova** .  
  
### <a name="bookmarks"></a>Segnalibri  
 Per tornare più facilmente a una riga, è possibile creare un segnalibro per una o più righe nei dati di destinazione. Fare clic con il pulsante destro del mouse su una riga per modificare il segnalibro. Utilizzare i pulsanti Indietro e Avanti nella barra degli strumenti **Eventi estesi** per passare alle righe con segnalibro.  
  
### <a name="change-display-settings"></a>Modificare le impostazioni di visualizzazione  
 È possibile salvare le informazioni sulle colonne (ordine delle colonne, colonna di unione e larghezza delle colonne) e sul filtro di un risultato di traccia in un file di impostazioni di visualizzazione degli eventi estesi (con estensione viewsetting). Dopo aver salvato il file, è possibile applicarlo ai risultati della traccia per modificare la vista.  
  
 Per modificare le impostazioni di visualizzazione:  
  
1.  Aprire un file XEL per visualizzare i risultati della traccia. È anche possibile fare clic con il pulsante destro del mouse sul nome della sessione e scegliere **Controlla i dati dinamici**.  
  
2.  Nella barra degli strumenti **Eventi estesi** selezionare **Impostazioni visualizzazione**. Selezionare una delle opzioni seguenti nell'elenco a discesa:  
  
    -   Salva con nome. Consente di salvare le informazioni sulle colonne e sul filtro di un risultato di traccia in un file con estensione viewsetting.  
  
    -   Apertura. Consente di aprire un file con estensione viewsetting esistente.  
  
    -   Apri recenti. Consente di aprire un file con estensione viewsetting salvato recentemente.  
  
### <a name="copy-or-export-trace-results"></a>Copiare o esportare i risultati della traccia  
 È possibile copiare celle, righe e dettagli nelle righe selezionate dai risultati della traccia. È inoltre possibile esportare i risultati della traccia negli elementi seguenti:  
  
-   File XEL  
  
-   tabella  
  
-   File CSV  
  
 Per copiare i risultati della traccia, selezionare una cella, una o più righe, fare clic con il pulsante destro del mouse e scegliere **Copia** , quindi selezionare **Cella**, **Riga**o **Dettagli**. Eventi estesi supporta la copia di un massimo di 1000 righe.  
  
 È possibile esportare i risultati della traccia in un file XEL, una tabella o un file CSV selezionando **Esporta in** nell'opzione di menu **Eventi estesi** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
### <a name="view-a-deadlock-graph-and-query-plans"></a>Visualizzare un evento Deadlock Graph e piani di query  
 È possibile visualizzare l'evento Deadlock Graph per **xml_deadlock_report** nel riquadro Dettagli per consentire di risolvere i problemi relativi ai deadlock. È anche possibile visualizzare i grafici del piano di query per gli eventi seguenti:  
  
-   query_post_compilation_showplan  
  
-   query_pre_execution_showplan  
  
-   query_post_execution_showplan  
  
 Per visualizzare l'evento Deadlock Graph:  
  
-   In Esplora oggetti espandere i nodi **Gestione**, **Eventi estesi**, quindi **Sessioni** .  
  
-   Fare clic con il pulsante destro del mouse sulla sessione in cui è contenuto l'evento deadlock configurato che si desidera visualizzare e scegliere **Controlla i dati dinamici**.  
  
-   Selezionare l'evento deadlock e visualizzare il grafico nella scheda **Deadlock** nel riquadro Dettagli.  
  
 Per visualizzare i grafici del piano di query:  
  
1.  In Esplora oggetti espandere i nodi **Gestione**, **Eventi estesi**, quindi **Sessioni** .  
  
2.  Fare clic con il pulsante destro del mouse sulla sessione in cui è contenuto il grafico del piano di query che si desidera visualizzare, ad esempio query_post_compilation_showplan, quindi scegliere **Controlla i dati dinamici**.  
  
3.  Selezionare l'evento grafico del piano di query, ad esempio query_post_compilation_showplan, e visualizzare il grafico sulla scheda **Piano query** nel riquadro Dettagli.  
  
  
