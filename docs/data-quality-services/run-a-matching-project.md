---
title: Eseguire un progetto corrispondente
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.matchingproject.map.f1
- sql13.dqs.matchingproject.matching.f1
- sql13.dqs.matchingproject.export.f1
ms.assetid: 6aa9d199-83ce-4b5d-8497-71eef9258745
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 473b30d2dcc4809feece4e6a1cc59e38bb82ac2e
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75244116"
---
# <a name="run-a-matching-project"></a>Eseguire un progetto corrispondente

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  In questo argomento viene descritto come eseguire la corrispondenza dei dati in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Il processo di corrispondenza identifica i cluster di record corrispondenti in base alle regole di corrispondenza nei criteri di corrispondenza, definisce un record da ogni cluster come superstite in base a una regola di sopravvivenza ed esporta i risultati. In DQS il processo di corrispondenza, definito anche deduplicazione, è computerizzato ma è possibile creare alcune regole di corrispondenza in modo interattivo e selezionare la regola di sopravvivenza tra diverse opzioni, in modo da controllare comunque il processo.  
  
 La corrispondenza viene eseguita in tre fasi: un processo di mapping in cui si identifica l'origine dati e si esegue il mapping dei domini all'origine dati; un processo di corrispondenza in cui si esegue l'analisi di corrispondenza; un processo di sopravvivenza ed esportazione in cui si definisce la regola di sopravvivenza e si esportano i risultati di corrispondenza. Ognuno di questi processi viene eseguito in una pagina separata della procedura guidata relativa all'attività di corrispondenza, consentendo all'utente di spostarsi da una pagina a un'altra al fine di rieseguire il processo, completare un processo di corrispondenza specifico e tornare nuovamente a una fase specifica. DQS fornisce statistiche relative ai dati di origine, alle regole e ai risultati di corrispondenza. Tali statistiche consentono di prendere decisioni informate sulla corrispondenza e di ridefinire il processo di corrispondenza.  
  
 La preparazione del processo di corrispondenza prevede la creazione dei criteri di corrispondenza con uno o più regole di corrispondenza e l'esecuzione dei criteri sui dati di esempio. Il processo del progetto corrispondente è diverso dal processo per i criteri di corrispondenza in quanto la Knowledge Base non viene popolata con le informazioni di corrispondenza ottenute dal progetto corrispondente. Per ulteriori informazioni sulla creazione dei criteri di corrispondenza, vedere [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="BeforeYouBegin"></a>Prima di iniziare  
  
###  <a name="Prerequisites"></a>Prerequisiti  
  
-   È necessario avere creato una Knowledge Base con criteri di corrispondenza composti da una o più regole di corrispondenza.  
  
-   Se i dati di origine per la corrispondenza si trovano in un file di Excel, è necessario che Microsoft Excel sia installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . In caso contrario, non sarà possibile selezionare il file di Excel nella fase di mapping. I file creati da Microsoft Excel potranno presentare l'estensione xlsx, xls o csv. Se viene utilizzata la versione a 64 bit di Excel, sono supportati solo i file di Excel 2003 (xls), mentre non sono supportati file di Excel 2007 o 2010 (xlsx). Se si utilizza una versione a 64 bit di Excel 2007 o 2010, salvare il file come file xls o csv o installare una versione a 32 bit di Excel.  
  
###  <a name="Security"></a>Sicurezza  
  
####  <a name="Permissions"></a>Autorizzazioni  
 Per eseguire un progetto corrispondente, è necessario disporre del ruolo dqs_kb_editor o dqs_administrator nel database DQS_MAIN.  
  
##  <a name="StartingaMatchingProject"></a>Primo passaggio: avvio di un progetto corrispondente  
 L'attività di corrispondenza viene eseguita in un progetto Data Quality creato nell'applicazione client DQS.  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Eseguire l'applicazione Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Nella schermata iniziale del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] fare clic su **Nuovo progetto Data Quality** per eseguire la corrispondenza in un nuovo progetto Data Quality. Immettere un nome per il progetto Data Quality, immettere una descrizione e selezionare la Knowledge Base che si desidera utilizzare per la corrispondenza in **Usa Knowledge Base**. Fare clic su **Corrispondenza** per l'attività. Fare clic su **Avanti** per passare alla fase di mapping.  
  
3.  Fare clic su **Apri progetto Data Quality** per eseguire la corrispondenza in un progetto Data Quality esistente. Selezionare il progetto, quindi fare clic su **Avanti**. In alternativa, è possibile fare clic su un progetto in **progetto Data Quality recente**. Se si apre un progetto corrispondente chiuso, si procederà con la fase in cui l'attività di progetto corrispondente è stata chiusa (come indicato dalla colonna **stato** nella tabella Project o nel nome del progetto in **progetto Data Quality recente**). Se si apre un progetto corrispondente completato, si passerà alla pagina **Esporta** e non sarà più possibile tornare alle schermate precedenti.  
  
##  <a name="MappingStage"></a>Fase di mapping  
 Nella fase di mapping si identifica l'origine dei dati in cui verrà eseguita l'analisi di corrispondenza e si esegue il mapping delle colonne di origine ai domini per rendere tali domini disponibili per l'attività di corrispondenza.  
  
1.  Nella pagina **Mappa** , per eseguire la corrispondenza su un database, lasciare selezionato **SQL Server** come **Origine dati**, selezionare il database su cui si desidera eseguire la corrispondenza, quindi selezionare la tabella. Il database di origine deve trovarsi nella stessa istanza di SQL Server del server DQS. in caso contrario, non verrà visualizzato nell'elenco a discesa.  
  
2.  Per eseguire la corrispondenza sui dati in un foglio di calcolo di Excel, selezionare **File di Excel** come **Origine dati**, fare clic su **Sfoglia** e selezionare il file di Excel, quindi lasciare selezionato **Utilizza la prima riga come intestazione** , se appropriato. In **Foglio di lavoro**selezionare il foglio di lavoro nel file di Excel che fungerà da origine dei dati. Per selezionare un file di Excel, è necessario che Excel sia installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] . Se Excel non è installato nel computer del [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , il pulsante **Sfoglia** non sarà disponibile e verrà visualizzata una notifica sotto questa casella di testo in cui si avvisa che Excel non è installato.  
  
3.  In **Mapping**, selezionare un campo nell'origine dati per **Colonna di origine**, quindi selezionare il dominio corrispondente. Ripetere l'operazione per tutti i domini da utilizzare per il processo di corrispondenza. È necessario che per ogni dominio definito nei criteri di corrispondenza venga eseguito il mapping alla colonna di origine appropriata. Nel riquadro destro della pagina Mappa vengono visualizzati i domini definiti nei criteri di corrispondenza e le relative regole.  
  
    > [!NOTE]  
    >  È possibile eseguire il mapping dei dati di origine a un dominio DQS solo se il tipo di dati di origine è supportato in DQS e corrisponde al tipo di dati del dominio DQS. Per ulteriori informazioni sui tipi di dati supportati in DQS, vedere [Tipi di dati di SQL Server e SSIS supportati per i domini DQS](../data-quality-services/supported-sql-server-and-ssis-data-types-for-dqs-domains.md).  
  
4.  Fare clic sul controllo **Più (+)** per aggiungere una riga alla tabella Mapping o sul controllo **Meno (-)** per rimuovere una riga.  
  
5.  Fare clic su **Anteprima origine dati** per visualizzare i dati nella tabella o vista di SQL Server selezionata o nel foglio di lavoro di Excel selezionato.  
  
6.  Fare clic su **Visualizza/Seleziona domini compositi** per visualizzare un elenco dei domini compositi disponibili nella Knowledge Base e selezionarli in base alle esigenze per l'esecuzione del mapping.  
  
7.  Fare clic su **Avanti** per passare alla fase di corrispondenza.  
  
    > [!NOTE]  
    >  Fare clic su **Chiudi** per salvare la fase del progetto di corrispondenza e tornare alla home page di DQS. Alla successiva apertura, il progetto verrà avviato dalla stessa fase. Fare clic su **Annulla** per terminare l'attività di corrispondenza e tornare alla home page di DQS.  
  
##  <a name="MatchingStage"></a>Fase corrispondente  
 In questa fase si esegue un processo di corrispondenza computerizzato che indica il numero di corrispondenze presenti nei dati di origine in base alle regole di corrispondenza. Questo processo genererà una tabella dei risultati di corrispondenza in cui vengono mostrati i cluster identificati da DQS, ogni record presente nel cluster con il relativo ID e il punteggio corrispondente nonché il record iniziale per il cluster. Il record iniziale nel cluster viene selezionato casualmente. Il record superstite viene determinato selezionando la regola di sopravvivenza nella pagina **Esporta** quando si esegue il progetto corrispondente. Ogni riga aggiuntiva in un cluster viene considerata una corrispondenza; il punteggio corrispondente, rispetto al record iniziale, viene riportato nella tabella dei risultati. Il numero del cluster corrisponde all'ID record relativo al record iniziale del cluster.  
  
 Nei risultati di corrispondenza è possibile applicare un filtro per i dati desiderati e rifiutare le corrispondenze non desiderate. È possibile visualizzare i dati di profiling per il processo di corrispondenza nel loro insieme, le specifiche sulle regole di corrispondenza applicate e le statistiche sui risultati di corrispondenza nel loro insieme. Il processo di corrispondenza può identificare i cluster sovrapposti e quelli non sovrapposti e in caso di più esecuzioni può essere eseguito sui dati appena copiati dall'origine e reindicizzati o sui dati precedenti.  
  
1.  Nella pagina **Corrispondenza**selezionare **Cluster sovrapposti** dall'elenco a discesa per visualizzare i record pivot e i record successivi per tutti i cluster quando viene eseguita la corrispondenza, anche qualora i gruppi di cluster presentino record in comune. Selezionare **Cluster non sovrapposti** per visualizzare i cluster che presentano record in comune come cluster singolo all'esecuzione della corrispondenza.  
  
2.  Fare clic su **Ricarica dati di origine** (valore predefinito) per copiare i dati dall'origine dati nella tabella di staging e reindicizzarli quando si esegue il progetto corrispondente. Fare clic su **Esegui sui dati precedenti** per eseguire il progetto corrispondente senza copiare i dati nella tabella di staging e senza reindicizzare i dati. **Esegui sui dati precedenti** è disabilitato per la prima esecuzione del progetto corrispondente o se si modifica il mapping nella pagina **Mappa** e si preme **Sì** nel popup seguente. In entrambi tali casi, è necessario effettuare la reindicizzazione. Se il progetto corrispondente non viene modificato, non è necessaria alcuna reindicizzazione. L'esecuzione sui dati precedenti può migliorare le prestazioni.  
  
3.  Fare clic su **Avvia** per avviare la corrispondenza sull'origine dati selezionata.  
  
4.  Fare clic su **Arresta** se si desidera arrestare il progetto corrispondente ed eliminare i risultati.  
  
5.  Al termine del processo di corrispondenza verificare che i cluster nella tabella **Risultati corrispondenza** siano appropriati e visualizzare le statistiche nelle schede **Profiler** e **Risultati corrispondenza** per assicurarsi di avere ottenuto i risultati desiderati. Visualizzare i record corrispondenti selezionando **Con corrispondenza** per **Filtro** oppure visualizzare i record non corrispondenti selezionando **Senza corrispondenza**.  
  
6.  Se si dispone di più regole di corrispondenza nei criteri di corrispondenza, fare clic sulla scheda **Regole di corrispondenza** per identificare l'icona per ogni regola, quindi verificare quale regola ha identificato un record come corrispondenza identificando la regola nella colonna **Regola** della tabella **Risultati corrispondenza** .  
  
7.  Se si seleziona un record non pivot nella tabella e si fa clic sull'icona **Visualizza dettagli** , o si fa doppio clic sul record, in DQS viene visualizzata la finestra popup **Dettagli punteggio corrispondente** in cui sono visibili il record su cui si è fatto doppio clic e il relativo record pivot, nonché i valori in tutti i relativi campi, il punteggio tra tali record e un drill-down dei contributi del punteggio corrispondente di ciascun campo. Se si fa doppio clic su un record pivot, non verrà visualizzata alcuna finestra popup.  
  
8.  Fare clic sull'icona **Comprimi tutto** per comprimere i record visualizzati nella tabella **Risultati corrispondenza** per includere solo i record pivot e non i record duplicati. Fare clic sull'icona **Espandi tutto** per espandere i record visualizzati nella tabella Risultati corrispondenza per includere tutti i record duplicati.  
  
9. Per rifiutare un record dai risultati corrispondenti, fare clic sulla casella di controllo **Rifiutato** del record.  
  
10. Per modificare il punteggio corrispondente minimo che determina il livello di corrispondenza da applicare a un record perché questo venga visualizzato, selezionare l'icona **Punteggio corrispondente minimo** sul lato destro della tabella e immettere un numero maggiore. Il punteggio corrispondente minimo è impostato su 80% per impostazione predefinita. Fare clic su **Aggiorna** per modificare il contenuto della tabella.  
  
11. Una volta completata l'analisi, il pulsante **Avvia** viene sostituito dal pulsante **Riavvia** . Fare clic su **Riavvia** per eseguire di nuovo il progetto di analisi. Se i risultati dall'analisi precedente non sono stati ancora salvati, facendo clic su **Riavvia** si causerà la perdita di tali dati non salvati. Per continuare, fare clic su **Sì** nella finestra popup. Durante l'esecuzione dell'analisi, non lasciare la pagina o il processo di analisi verrà interrotto.  
  
12. Fare clic su **Avanti** per passare alla fase di sopravvivenza e di esportazione.  
  
##  <a name="SurvivorshipandExportStage"></a>Fase di sopravvivenza e di esportazione  
 Nel processo di sopravvivenza Data Quality Services consente di determinare un record superstite per ogni cluster, che sostituirà gli altri record corrispondenti nel cluster. I risultati di sopravvivenza e/o di corrispondenza vengono quindi esportati in una tabella del database di SQL Server, in un file CSV o in un file di Excel.  
  
 La sopravvivenza è facoltativa. È possibile esportare i risultati senza eseguire la sopravvivenza. In tal caso viene utilizzato il record pivot definito nell'analisi di corrispondenza. Se due o più record in un cluster soddisfano la regola di sopravvivenza, il processo di sopravvivenza selezionerà l'ID record minore tra i record in conflitto come superstite. È possibile esportare i superstiti in diversi file o tabelle utilizzando regole di sopravvivenza diverse.  
  
1.  Nella pagina **Esporta** selezionare la destinazione in cui si desidera esportare i dati corrispondenti in **Tipo destinazione**, scegliendo tra **SQL Server**, **File CSV**o **File di Excel**.  
  
    > [!IMPORTANT]  
    >  Se si utilizza la versione a 64 bit di Excel, non è possibile esportare i dati corrispondenti in un file di Excel. È possibile eseguire l'esportazione solo in un database di SQL Server o in un file con estensione csv.  
  
2.  Se è stato selezionato **SQL Server** per **Tipo destinazione**, selezionare il database in cui esportare i risultati in **Nome database**.  
  
    > [!IMPORTANT]  
    >  Il database di destinazione deve trovarsi nella stessa istanza di SQL Server del server DQS. in caso contrario, non verrà visualizzato nell'elenco a discesa.  
  
3.  Selezionare la casella di controllo per **Risultati corrispondenza** per esportare i risultati corrispondenti (vedere la descrizione riportata in precedenza) nella tabella definita in un database di SQL Server o nel file CSV o di Excel specificato. Selezionare la casella di controllo per **Risultati sopravvivenza** per esportare i risultati di sopravvivenza (vedere la descrizione riportata in precedenza) nella tabella definita in un database di SQL Server o nel file CSV o di Excel specificato.  
  
     Per i risultati corrispondenti verranno esportati gli elementi seguenti:  
  
    -   Un elenco di cluster con i record corrispondenti in ogni cluster, inclusi il nome della regola e il punteggio. Il record pivot sarà contrassegnato come "Pivot". I cluster verranno visualizzati per primi nell'elenco di esportazione.  
  
    -   Un elenco di record non corrispondenti con "NULL" nelle colonne Punteggio e Nome regola. Questi record verranno aggiunti nell'elenco di esportazione dopo i cluster.  
  
     Per i risultati di sopravvivenza verranno esportati gli elementi seguenti:  
  
    -   Un elenco di record superstiti come stabilito dal processo di sopravvivenza in base alla regola di sopravvivenza. Questi record verranno visualizzati per primi nell'elenco di esportazione.  
  
    -   Un elenco di record non corrispondenti non inclusi nei cluster di record corrispondenti. Questi record vengono aggiunti dopo i risultati dei record superstiti.  
  
4.  Se è stato selezionato **SQL Server** per **Tipo destinazione**, immettere il nome delle tabelle in cui si desidera esportare i risultati in **Nome tabella**. Se si esportano sia i risultati corrispondenti che quelli di sopravvivenza, le tabelle di destinazione devono avere nomi diversi essendo univoche nel database.  
  
5.  Se è stato selezionato **File CSV** per **Tipo destinazione**, immettere il nome e il percorso del file CSV in cui si desidera esportare i risultati in **Nome file CSV**.  
  
6.  Se è stato selezionato **File di Excel** per **Tipo destinazione**, immettere il nome e il percorso del file di Excel in cui si desidera esportare i risultati in **Nome del file di Excel**. Non è possibile esportare in un file di Excel se si utilizza la versione a 64 bit di Excel.  
  
7.  Selezionare la regola di sopravvivenza come segue:  
  
    -   Selezionare **Record pivot** (valore predefinito) per identificare il record superstite come record pivot iniziale scelto arbitrariamente da DQS.  
  
    -   Selezionare **Il record più completo e più lungo** per identificare il record superstite come il record con il maggior numero di campi popolati e con il maggior numero di termini in ogni campo. Vengono controllati tutti i campi di origine, anche quelli di cui non è stato eseguito il mapping a un dominio nella pagina **mappa** .  
  
    -   Selezionare **Record più completo** per identificare il record superstite come il record con il maggior numero di campi popolati. Un campo popolato contiene almeno un valore (valori stringa o numerici oppure entrambi). Vengono controllati tutti i campi di origine, anche quelli di cui non è stato eseguito il mapping a un dominio nella pagina Mappa. Un campo popolato contiene almeno un valore (valori stringa o numerici oppure entrambi).  
  
    -   Selezionare **Record più lungo** per identificare il record superstite come il record con il maggior numero di termini nei relativi campi di origine. Per determinare la lunghezza di ogni record, in DQS viene verificata la lunghezza dei termini in tutti i campi di origine, anche in quelli di cui non è stato eseguito il mapping a un dominio nella pagina **Mappa** .  
  
8.  Visualizzare le statistiche nella scheda **Profiler** per assicurarsi di avere ottenuto i risultati desiderati.  
  
9. Fare clic su **Esporta** per esportare i risultati. Verrà visualizzata la finestra di dialogo Esportazione corrispondenze in cui viene indicato lo stato di avanzamento e quindi i risultati dell'esportazione.  
  
    -   Se è stato selezionato **SQL Server** come destinazione dei dati, nel database selezionato verrà creata una nuova tabella con il nome specificato.  
  
    -   Se è stato selezionato **File CSV** come destinazione dei dati, verrà creato un file CSV nel percorso del computer del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con il nome file specificato in precedenza nella casella **Nome file CSV** .  
  
    -   Se è stato selezionato **File di Excel** come destinazione dei dati, verrà creato un file XLSX nel percorso del computer del [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)] con il nome file specificato in precedenza nella casella **Nome file di Excel** .  
  
10. Verificare che l'esportazione venga completata correttamente, quindi fare clic su **Chiudi**.  
  
11. Fare clic su **Fine** per completare il progetto corrispondente.  
  
    > [!NOTE]  
    >  Se un progetto corrispondente viene completato e quindi riutilizzato, verrà utilizzata la stessa Knowledge Base di quando il progetto è stato pubblicato. Non verrà utilizzata alcuna modifica apportata alla Knowledge Base dopo il completamento del progetto. Per utilizzare tali modifiche o una nuova Knowledge Base, sarà necessario creare un nuovo progetto corrispondente. Se invece il progetto corrispondente è stato creato ma non completato, verranno utilizzate tutte le modifiche pubblicate nei criteri di corrispondenza quando si esegue la corrispondenza nel progetto.  
  
##  <a name="FollowUp"></a>Completamento: fasi successive all'esecuzione di un progetto corrispondente  
 Dopo avere eseguito un progetto corrispondente, è possibile modificare i criteri di corrispondenza nella Knowledge Base e creare ed eseguire un altro progetto corrispondente in base ai criteri di corrispondenza aggiornati. Per altre informazioni, vedere [Create a Matching Policy](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="Profiler"></a>Schede Profiler e risultati  
 Le schede Profiler e Risultati contengono le statistiche del processo di corrispondenza.  
  
### <a name="profiler-tab"></a>Scheda Profiler  
 Fare clic sulla scheda **Profiler** per visualizzare statistiche per il database di origine e per ogni campo incluso nella regola dei criteri. Le statistiche verranno aggiornate all'esecuzione della regola dei criteri. Il profiling consente di valutare il livello di efficacia del processo di deduplicazione, determinando in che misura tale processo è in grado di migliorare la qualità dei dati. L'accuratezza nel profiling non è importante per un progetto corrispondente.  
  
 Le statistiche relative al database di origine includono:  
  
-   **Record**: numero totale di record nel database  
  
-   **Valori totali**: numero totale di valori nei campi  
  
-   **Nuovi valori**: numero totale di valori nuovi dall'esecuzione precedente e relativa percentuale dell'intero  
  
-   **Valori univoci**: numero totale di valori univoci nei campi e relativa percentuale dell'intero  
  
-   **Nuovi valori univoci**: numero totale di valori univoci nuovi nei campi e relativa percentuale dell'intero  
  
 Le statistiche relative ai campi includono:  
  
-   **Field**: nome del campo incluso nei mapping.  
  
-   **Dominio**: nome del dominio di cui è stato eseguito il mapping al campo.  
  
-   **Nuovo**: numero di nuove corrispondenze trovate e relativa percentuale del totale  
  
-   **Unique**: numero di record univoci nel campo e relativa percentuale del totale  
  
-   **Completezza**: percentuale di completamento dell'esecuzione della regola.  
  
### <a name="matching-policy-notifications"></a>Notifiche relative ai criteri di corrispondenza  
 Per l'attività relativa ai criteri di corrispondenza, le condizioni seguenti generano notifiche:  
  
-   Il campo è vuoto in tutti i record; è consigliabile eliminarlo dal mapping.  
  
-   Il punteggio di completezza del campo è molto basso; è consigliabile eliminarlo dal mapping.  
  
-   Un campo contiene solo valori non validi; è necessario verificare il mapping e la rilevanza delle regole di dominio sul contenuto del campo.  
  
-   Un campo contiene un basso livello di valori validi; è necessario verificare il mapping e la rilevanza delle regole di dominio sul contenuto del campo.  
  
-   Vi è un livello elevato di unicità nel campo. L'utilizzo del campo nei criteri di corrispondenza può diminuire i risultati di corrispondenza.  
  
### <a name="matching-rules-tab"></a>Scheda Regole di corrispondenza  
 Fare clic su questa scheda per visualizzare un elenco di regole nei criteri di corrispondenza e le condizioni in una regola.  
  
 **Elenco regole**  
 Visualizza un elenco di tutte le regole di corrispondenza nei criteri di corrispondenza. Selezionare una delle regole per visualizzare le condizioni nella regola nella tabella delle regole di corrispondenza.  
  
 **Tabella delle regole di corrispondenza**  
 Visualizza ogni condizione nella regola selezionata, inclusi dominio, valore di somiglianza, peso e prerequisito.  
  
### <a name="matching-results-tab"></a>Scheda Risultati corrispondenza  
 Fare clic sulla scheda **Risultati corrispondenza** per visualizzare le statistiche dell'analisi dell'origine dati utilizzando la Knowledge Base selezionata per il progetto e la regola o le regole di corrispondenza presenti nella Knowledge Base. Le statistiche includono gli elementi seguenti:  
  
-   Numero complessivo di record nel database  
  
-   Numero complessivo di record corrispondenti nel database  
  
-   Numero di record nel database che non si considerano duplicati  
  
-   Numero di cluster individuati  
  
-   Dimensione media di un cluster (numero di record duplicati diviso numero di cluster)  
  
-   Il minor numero di duplicati in un cluster  
  
-   Il maggior numero di duplicati in un cluster  
  
  
