---
title: Visualizzare e usare l'output di Ottimizzazione guidata motore di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql12.dta.reports.f1
- sql12.dta.sessionmonitor.f1
- sql12.dta.recommendations.f1
- sql12.dta.applyrecommendations.f1
helpviewer_keywords:
- viewing logs
- recommendations [Database Engine Tuning Advisor]
- summary tuning information [SQL Server]
- Database Engine Tuning Advisor [SQL Server], recommendations
- Database Engine Tuning Advisor [SQL Server], logs
- Database Engine Tuning Advisor [SQL Server], viewing output
- Database Engine Tuning Advisor [SQL Server], reports
- logs [SQL Server], tuning
- reports [SQL Server], tuning
- viewing tuning output
ms.assetid: 47f9d9a7-80b0-416d-9d9a-9e265bc190dc
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 29dac7e1636026da3f77ac832a148a832abe240a
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53356736"
---
# <a name="view-and-work-with-the-output-from-the-database-engine-tuning-advisor"></a>Visualizzare e utilizzare l'output di Ottimizzazione guidata motore di database
  Durante l'ottimizzazione di database tramite Ottimizzazione guidata motore di database, vengono creati automaticamente riepiloghi, indicazioni, report e log di ottimizzazione. È possibile utilizzare l'output del log di ottimizzazione per risolvere gli eventuali problemi verificatisi durante le sessioni di ottimizzazione di Ottimizzazione guidata motore di database. È possibile utilizzare i riepiloghi, le indicazioni e i report per determinare se implementare le indicazioni o continuare l'ottimizzazione fino a migliorare le prestazioni di esecuzione delle query come necessario per l'installazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per informazioni sull'utilizzo di Ottimizzazione guidata motore di database per creare carichi di lavoro e ottimizzare un database, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
##  <a name="View"></a> Visualizzazione output di ottimizzazione  
 Nelle procedure indicate di seguito viene illustrata la visualizzazione di indicazioni, riepiloghi, report e log di ottimizzazione tramite l'interfaccia utente grafica (GUI) di Ottimizzazione guidata motore di database. Per ulteriori informazioni sulle opzioni dell'interfaccia utente, vedere [Descrizioni dell'interfaccia utente](#UI) più avanti in questo argomento.  
  
 È possibile usare la GUI anche per visualizzare l'output dell'ottimizzazione generato dall'utilità della riga di comando **dta** .  
  
> [!NOTE]  
>  Se si usa l'utilità della riga di comando **dta** e si specifica che l'output venga scritto in un file XML con l'argomento **-ox** , sarà possibile aprire e visualizzare il file di output XML scegliendo **Apri file** dal menu **File** di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni, vedere [Use SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md). Per informazioni sull'utilità della riga di comando **dta** , vedere [Utilità dta](../../tools/dta/dta-utility.md).  
  
#### <a name="to-view-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Per visualizzare le indicazioni relative all'ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database  
  
1.  Ottimizzare un database usando la GUI di Ottimizzazione guidata motore di database o l'utilità da riga di comando **dta** . Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Se si desidera utilizzare una sessione di ottimizzazione esistente, ignorare questo passaggio e continuare con il passaggio 2.  
  
2.  Avviare la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Se si vuole visualizzare le indicazioni relative a una sessione di ottimizzazione esistente, aprire la sessione facendo doppio clic sul nome nella finestra **Monitoraggio sessione**.  
  
     Al termine della nuova sessione di ottimizzazione oppure dopo aver caricato la sessione esistente tramite lo strumento, verrà visualizzata la pagina **Indicazioni** .  
  
3.  Nella pagina **Indicazioni** fare clic su **Indicazioni relative alle partizioni** e **Indicazioni relative agli indici** per visualizzare i riquadri contenenti i risultati della sessione di ottimizzazione. Se non si è specificato il partizionamento quando sono state impostate le opzioni di ottimizzazione per la sessione, il riquadro **Indicazioni relative alle partizioni** sarà vuoto.  
  
4.  Nel riquadro **Indicazioni relative alle partizioni** o **Indicazioni relative agli indici** utilizzare le barre di scorrimento per visualizzare tutte le informazioni disponibili nella griglia.  
  
5.  Deselezionare **Mostra oggetti esistenti** nella parte inferiore della pagina a schede **Indicazioni** . Nella griglia verranno visualizzati solo gli oggetti di database cui si fa riferimento nell'indicazione. Usare la barra di scorrimento inferiore per visualizzare la colonna all'estremità destra nella griglia delle indicazioni e fare clic nella colonna **Definizione** per visualizzare o copiare lo script [!INCLUDE[tsql](../../includes/tsql-md.md)] che crea l'oggetto nel database.  
  
6.  Se si desidera salvare tutti gli script [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite cui vengono creati o eliminati tutti gli oggetti di database nell'indicazione in un file script, scegliere **Salva indicazioni** dal menu **Azioni** .  
  
#### <a name="to-view-the-tuning-summary-and-reports-with-the-database-engine-tuning-advisor-gui"></a>Per visualizzare il riepilogo e i report relativi all'ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database  
  
1.  Ottimizzare un database usando la GUI di Ottimizzazione guidata motore di database o l'utilità da riga di comando **dta** . Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Se si desidera utilizzare una sessione di ottimizzazione esistente, ignorare questo passaggio e continuare con il passaggio 2.  
  
2.  Avviare la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Per visualizzare i riepiloghi e i report relativi a una sessione di ottimizzazione esistente, aprire la sessione facendo doppio clic sul nome nella finestra **Monitoraggio sessione**.  
  
3.  Al termine della nuova sessione di ottimizzazione oppure dopo che tramite lo strumento è stata caricata la sessione esistente, selezionare la scheda **Report** .  
  
4.  Nel riquadro **Riepilogo ottimizzazione** sono incluse le informazioni relative alla sessione di ottimizzazione. Le informazioni contenute nelle voci **Miglioramento percentuale previsto** e **Spazio utilizzato seguendo le indicazioni (MB)** possono essere particolarmente utili per decidere se implementare o meno l'indicazione.  
  
5.  Nel riquadro **Report ottimizzazione** fare clic su **Selezionare il report** per specificare un report di ottimizzazione da visualizzare.  
  
#### <a name="to-view-tuning-logs-with-the-database-engine-tuning-advisor-gui"></a>Per visualizzare i log di ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database  
  
1.  Ottimizzare un database usando la GUI di Ottimizzazione guidata motore di database o l'utilità da riga di comando **dta** . Verificare di avere selezionato l'opzione **Salva log di ottimizzazione** nella scheda **Generale** quando si ottimizza il carico di lavoro. Se si desidera utilizzare una sessione di ottimizzazione esistente, ignorare questo passaggio e continuare con il passaggio 2.  
  
2.  Avviare la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Per visualizzare i riepiloghi e i report relativi a una sessione di ottimizzazione esistente, aprirla facendo doppio clic sul nome della sessione nella finestra **Monitoraggio sessione** .  
  
3.  Al termine della nuova sessione di ottimizzazione oppure dopo che tramite lo strumento è stata caricata la sessione esistente, selezionare la scheda **Stato** . Nel riquadro **Log di ottimizzazione** verrà visualizzato il contenuto del log. Nel log sono incluse le informazioni relative agli eventi del carico di lavoro che non è stato possibile analizzare tramite Ottimizzazione guidata motore di database.  
  
     Se tutti gli eventi nella sessione di ottimizzazione sono stati analizzati tramite Ottimizzazione guidata motore di database, viene visualizzato un messaggio indicante che il log di ottimizzazione è vuoto per la sessione. Se l'opzione **Salva log di ottimizzazione** non è stata selezionata nella scheda **Generale** quando la sessione di ottimizzazione originale è stata eseguita, viene visualizzato un messaggio indicante questo aspetto.  
  
##  <a name="Implement"></a> implementazione delle indicazioni di ottimizzazione  
 È possibile implementare le indicazioni di Ottimizzazione guidata motore di database manualmente oppure automaticamente come parte della sessione di ottimizzazione. Per esaminare i risultati dell'ottimizzazione prima di implementarli, utilizzare la GUI di Ottimizzazione guidata motore di database. È quindi possibile utilizzare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per eseguire manualmente gli script [!INCLUDE[tsql](../../includes/tsql-md.md)] generati da Ottimizzazione guidata motore di database come risultato dell'analisi di un carico di lavoro per implementare le raccomandazioni. Se non è necessario esaminare i risultati prima di implementarli, è possibile usare l'opzione **-a** con l'utilità del prompt dei comandi **dta** . In tal modo l'utilità implementa automaticamente le indicazioni di ottimizzazione dopo che analizza il carico di lavoro. Nelle procedure seguenti viene illustrato come utilizzare entrambe le interfacce di Ottimizzazione guidata motore di database per implementare le indicazioni relative all'ottimizzazione.  
  
#### <a name="to-manually-implement-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Per implementare manualmente le indicazioni relative all'ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database  
  
1.  Ottimizzare un database usando la GUI di Ottimizzazione guidata motore di database o l'utilità del prompt dei comandi **dta** . Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Se si desidera utilizzare una sessione di ottimizzazione esistente, ignorare questo passaggio e continuare con il passaggio 2.  
  
2.  Avviare la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Per implementare le indicazioni relative a una sessione di ottimizzazione esistente, aprirla facendo doppio clic sul nome della sessione in **Monitoraggio sessione**.  
  
3.  Al termine della nuova sessione di ottimizzazione oppure dopo il caricamento della sessione esistente da parte dello strumento, scegliere **Applica indicazioni** dal menu **Azioni** .  
  
4.  Nella finestra di dialogo **Applica indicazioni** scegliere **Applica ora** o **Pianifica per un momento successivo**. Se si sceglie l'opzione **Pianifica per un momento successivo**, selezionare la data e l'ora appropriate.  
  
5.  Fare clic su **OK** per applicare le indicazioni.  
  
#### <a name="to-automatically-implement-tuning-recommendations-using-the-dta-command-prompt-utility"></a>Per implementare automaticamente le indicazioni relative all'ottimizzazione tramite l'utilità della riga di comando dta  
  
1.  Stabilire quali funzionalità del database (indici, viste indicizzate, partizionamento) si desidera aggiungere, rimuovere o mantenere durante l'analisi eseguita con Ottimizzazione guidata motore di database.  
  
     Prima di iniziare l'ottimizzazione, prendere in considerazione quanto segue:  
  
    -   Quando come carico di lavoro si utilizza una tabella di traccia, è necessario che la tabella sia inclusa nel server in cui viene eseguito Ottimizzazione guidata motore di database. Se si crea una tabella di traccia su un altro server, spostarla nel server in cui viene eseguita l'ottimizzazione mediante Ottimizzazione guidata motore di database.  
  
    -   Se la durata dell'esecuzione di una sessione di ottimizzazione è superiore a quanto previsto, è possibile premere CTRL+C per interromperla. Se si preme CTRL+C in questa situazione, si forza **dta** a produrre le migliori indicazioni possibili in base alla quantità del carico di lavoro usata, in modo da non sprecare il tempo già impiegato dallo strumento per ottimizzare il carico di lavoro.  
  
2.  Dal prompt dei comandi digitare quanto segue:  
  
    ```  
    dta -E -D DatabaseName -if WorkloadFile -s SessionName -a  
    ```  
  
     dove **-E** specifica che la sessione di ottimizzazione usa una connessione trusted, invece di un ID di accesso e una password, **-D** specifica il nome del database da usare o un elenco delimitato da virgole di più database usati dal carico di lavoro, **-if** specifica il nome e il percorso di un file di carico di lavoro, **-s** specifica un nome per la sessione di ottimizzazione e **-a** specifica che si vuole che le indicazioni relative all'ottimizzazione vengano applicate automaticamente dall'utilità del prompt dei comandi **dta** senza richiedere l'intervento dell'utente al termine dell'analisi del carico di lavoro. Per altre informazioni sull'uso dell'utilità del prompt dei comandi **dta** per ottimizzare i database, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
3.  Premere INVIO.  
  
##  <a name="Analysis"></a> Esecuzione dell'analisi esplorativa  
 La funzionalità di configurazione specificata dall'utente di Ottimizzazione guidata motore di database consente agli amministratori di database di eseguire l'analisi esplorativa. Tramite questa funzionalità è possibile specificare la progettazione del database fisica in Ottimizzazione guidata motore di database e valutare quindi gli effetti di tale progettazione sulle prestazioni senza doverla implementare. La configurazione specificata dall'utente è supportata sia dall'interfaccia utente grafica (GUI) che dall'utilità da riga di comando di Ottimizzazione guidata motore di database. L'utilità da riga di comando offre tuttavia il livello di flessibilità maggiore.  
  
 Tramite la GUI è possibile valutare gli effetti ottenuti con l'implementazione di un subset di un'indicazione di ottimizzazione suggerita da Ottimizzazione guidata motore di database, mentre non è possibile aggiungere strutture di progettazione fisica ipotetiche per la valutazione in Ottimizzazione guidata.  
  
 Le procedure seguenti illustrano l'utilizzo della funzionalità in entrambe le interfacce dello strumento di ottimizzazione.  
  
### <a name="using-database-engine-tuning-advisor-gui-to-evaluate-tuning-recommendations"></a>Valutazione delle indicazioni di ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database  
 Questa procedura illustra come valutare un'indicazione generata da Ottimizzazione guidata motore di database tramite la GUI dello strumento, in cui tuttavia non è possibile specificare nuove strutture di progettazione fisica per la valutazione.  
  
##### <a name="to-evaluate-tuning-recommendations-with-the-database-engine-tuning-advisor-gui"></a>Per valutare indicazioni di ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database  
  
1.  Ottimizzare un database tramite la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Per valutare una sessione di ottimizzazione esistente, fare doppio clic sulla sessione in **Monitoraggio sessione**.  
  
2.  Nella scheda **Indicazioni** deselezionare le strutture di progettazione fisica consigliate che non si desidera utilizzare.  
  
3.  Scegliere **Valuta indicazioni** dal menu **Azioni**. Verrà avviata automaticamente una nuova sessione di ottimizzazione.  
  
4.  Digitare il nome della sessione in **Nome sessione**. Per visualizzare la configurazione della struttura di progettazione fisica del database da valutare, fare clic su **Fare clic qui per vedere la sezione di configurazione** nell'area **Descrizione** sulla parte inferiore della finestra dell'applicazione di Ottimizzazione guidata motore di database.  
  
5.  Fare clic sul pulsante **Avvia analisi** sulla barra degli strumenti. I risultati dell'ottimizzazione possono essere esaminati nella scheda **Indicazioni** .  
  
### <a name="using-database-engine-tuning-advisor-gui-to-export-tuning-session-results-for-what-if-tuning-analysis"></a>Esportazione dei risultati di una sessione di ottimizzazione tramite la GUI di Ottimizzazione guidata motore di database per analisi di simulazione  
 La procedura seguente descrive come esportare i risultati di una sessione di Ottimizzazione guidata motore di database in un file XML, che è quindi possibile modificare e ottimizzare con l'utilità della riga di comando **dta** . Ciò consente di eseguire l'analisi per l'ottimizzazione su nuove strutture di progettazione fisica ipotetiche evitando l'overhead associato all'implementazione delle strutture stesse nel database, in modo da determinare a priori se si ottengono i miglioramenti delle prestazioni necessari. L'uso della GUI di Ottimizzazione guidata motore di database per ottimizzare il database e la successiva esportazione dei risultati in un file con estensione **.xml** rappresenta un ottimo modo per gli utenti non esperti del linguaggio XML di sfruttare la flessibilità offerta dall'XML Schema di Ottimizzazione guidata motore di database per l'esecuzione dell'analisi di simulazione.  
  
##### <a name="to-export-tuning-session-results-from-the-database-engine-tuning-advisor-gui-for-what-if-analysis-with-the-dta-command-line-utility"></a>Per esportare i risultati della sessione di ottimizzazione dalla GUI di Ottimizzazione guidata motore di database per analisi di simulazione tramite l'utilità della riga di comando dta  
  
1.  Ottimizzare un database tramite la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md). Per valutare una sessione di ottimizzazione esistente, fare doppio clic sulla sessione in **Monitoraggio sessione**.  
  
2.  Scegliere **Esporta risultati sessione** dal menu **File** e salvare i risultati in un file XML.  
  
3.  Aprire il file XML creato nel passaggio 2 nell'editor XML o nell'editor di testo desiderato oppure in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Scorrere il contenuto del file fino a visualizzare l'elemento `Configuration`. Copiare la sezione dell'elemento `Configuration` e incollarla in un modello di file di input XML dopo l'elemento `TuningOptions`. Salvare il file di input XML.  
  
4.  Nell'elemento `TuningOptions` del file di input XML creato nel passaggio 3 specificare le opzioni di ottimizzazione desiderate, modificare la sezione dell'elemento `Configuration` aggiungendo o eliminando le strutture di progettazione fisica in modo appropriato per l'analisi specifica, salvare il file e convalidarlo in base all'XML Schema di Ottimizzazione guidata motore di database. Per informazioni sulla modifica di questo file XML, vedere [Guida di riferimento ai file di input XML &#40;Ottimizzazione guidata motore di database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
5.  Specificare il file XML creato nel passaggio 4 come input dell'utilità della riga di comando **dta** . Per informazioni sull'utilizzo di file di input di XML con questo strumento, vedere la sezione "Ottimizzazione di un database tramite l'utilità dta" in [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
### <a name="using-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Utilizzo della funzionalità di configurazione specificata dall'utente tramite l'utilità da riga di comando dta  
 Gli sviluppatori XML esperti possono creare un file di input XML di Ottimizzazione guidata motore di database, in cui è possibile specificare un carico di lavoro e una configurazione ipotetica di strutture di progettazione di database fisiche, ad esempio indici, viste indicizzate o partizionamento. Con l'utilità della riga di comando **dta** è quindi possibile analizzare gli effetti di questa configurazione ipotetica sulle prestazioni delle query per il database. Questa procedura è descritta di seguito in dettaglio.  
  
##### <a name="to-use-the-user-specified-configuration-feature-with-the-dta-command-line-utility"></a>Per utilizzare la funzionalità di configurazione specificata dall'utente tramite l'utilità da riga di comando dta  
  
1.  Creare un carico di lavoro di ottimizzazione. Per informazioni sull'esecuzione di questa operazione, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
2.  Copiare e incollare l'[Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md) in un editor XML o un editor di testo. Utilizzare questo codice di esempio per la creazione di un file di input XML per la sessione di ottimizzazione in corso. Per informazioni sull'esecuzione di questa attività, vedere la sezione "Creare un file di input XML" in [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
3.  Modificare gli elementi `TuningOptions` e `Configuration` del file di input XML di esempio. Nell'elemento `TuningOptions` specificare le strutture di progettazione fisica che devono essere prese in considerazione da Ottimizzazione guidata motore di database durante la sessione di ottimizzazione. Nell'elemento `Configuration` specificare le strutture di progettazione fisica corrispondenti alla configurazione ipotetica delle strutture di progettazione fisica del database che si desidera siano analizzate da Ottimizzazione guidata motore di database. Per informazioni sugli attributi e gli elementi figlio è possibile usare con il `TuningOptions` e il `Configuration` gli elementi padre, vedere [riferimento a File di Input XML &#40;Ottimizzazione guidata motore di Database&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md).  
  
4.  Salvare il file di input con l'estensione **xml** .  
  
5.  Convalidare il file di input XML salvato nel passaggio 4 in base all'XML Schema di Ottimizzazione guidata motore di database. Durante l'installazione di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]questo schema viene installato nella posizione seguente:  
  
    ```  
    C:\Program Files\Microsoft SQL Server\100\Tools\Binn\schemas\sqlserver\2004\07\dta\dtaschema.xsd  
    ```  
  
     XML Schema di Ottimizzazione guidata motore di database è anche disponibile online all'indirizzo [https://schemas.microsoft.com/sqlserver/2004/07/dta](https://schemas.microsoft.com/sqlserver/2004/07/dta).  
  
6.  Dopo aver creato un carico di lavoro e un file di input XML, è possibile specificare il file di input nell'utilità della riga di comando **dta** per eseguirne l'analisi. Assicurarsi di specificare un nome di file di output XML nell'argomento **-ox** . In tal modo viene creato un file di output XML con la configurazione indicata specificata nell'elemento `Configuration`. Se si desidera eseguire nuovamente Ottimizzazione guidata motore di database per verificare un'altra configurazione ipotetica basata sull'output, copiare il contenuto dell'elemento `Configuration` del file di output e incollarlo nel file di input XML originale o in un nuovo file XML. Per informazioni sull'uso di un file di input XML con l'utilità **dta** , vedere la sezione "Ottimizzazione di un database tramite l'utilità dta" in [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
     Dopo il completamento dell'ottimizzazione visualizzare i report dell'operazione nella GUI di Ottimizzazione guidata motore di database oppure aprire il file di output XML ed esaminare le indicazioni di Ottimizzazione guidata motore di database negli elementi `TuningSummary` e `Configuration`. Per informazioni sulla visualizzazione dei risultati della sessione di ottimizzazione, vedere [Visualizzazione output di ottimizzazione](#View) precedentemente in questo argomento. Si noti inoltre che i report di analisi potrebbero essere contenuti anche nel file di output XML.  
  
7.  Ripetere i passaggi 6 e 7 fino a creare la configurazione ipotetica che consente di ottenere i miglioramenti delle prestazioni di esecuzione delle query desiderati. È quindi possibile implementare la nuova configurazione. Per ulteriori informazioni, vedere [Implementazione delle indicazioni relative all'ottimizzazione](#Implement) più indietro in questo argomento.  
  
##  <a name="ReviewEvaluateClone"></a> Verifica, valutazione e clonazione delle sessioni di ottimizzazione  
 Ottimizzazione guidata motore di database crea una nuova sessione di ottimizzazione ogni volta che si avvia l'analisi dell'effetto di un carico di lavoro sul database o sui database. È possibile utilizzare il riquadro **Monitoraggio sessione** della GUI di Ottimizzazione guidata motore di database per visualizzare o ricaricare tutte le sessioni di ottimizzazione eseguite su una data istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La visualizzazione di tutte le sessioni di ottimizzazione esistenti per la verifica contribuisce a semplificare la clonazione di sessioni in base alle sessioni esistenti, la modifica di indicazioni esistenti sull'ottimizzazione e quindi l'utilizzo di Ottimizzazione guidata motore di database per valutare la sessione modificata oppure l'esecuzione dell'ottimizzazione a intervalli regolari per monitorare la struttura fisica dei database. Ad esempio, è possibile pianificare l'ottimizzazione dei database su base mensile.  
  
 Prima di verificare le sessioni di ottimizzazione per un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario creare sessioni di ottimizzazione sull'istanza del server, ottimizzando i carichi di lavoro tramite Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
### <a name="review-existing-tuning-sessions"></a>Verifica delle sessioni di ottimizzazione esistenti  
 Per sfogliare le sessioni di ottimizzazione esistenti in una determinata istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], eseguire la procedura seguente.  
  
##### <a name="to-review-existing-tuning-sessions"></a>Per verificare le sessioni di ottimizzazione esistenti  
  
1.  Avviare la GUI di Ottimizzazione guidata motore di database. Per altre informazioni, vedere [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md).  
  
2.  Tutte le sessioni di ottimizzazione esistenti vengono visualizzate nella parte superiore della finestra **Monitoraggio sessione** . Il numero di sessioni visualizzate dipende dal numero di ottimizzazioni dei database eseguite in questa istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Utilizzare le barre di scorrimento per visualizzare tutte le sessioni di ottimizzazione.  
  
3.  Se si fa clic sul nome di una sessione di ottimizzazione, i dettagli relativi a tale sessione verranno visualizzati nella parte inferiore della finestra **Monitoraggio sessione** .  
  
4.  Se si fa doppio clic sul nome di una sessione di ottimizzazione, le informazioni relative a tale sessione verranno caricate in Ottimizzazione guidata motore di database. Al termine del caricamento delle informazioni sulla sessione è possibile scegliere una delle schede disponibili per visualizzare le informazioni sulla sessione di ottimizzazione specifica.  
  
### <a name="evaluate-existing-tuning-sessions-as-hypothetical-configurations"></a>Valutazione delle sessioni di ottimizzazione esistenti come configurazioni ipotetiche  
 Per valutare una sessione di ottimizzazione esistente, eseguire la procedura seguente. La valutazione di una sessione di ottimizzazione esistente comporta la visualizzazione e la modifica delle indicazioni relative a tale sessione e quindi la ripetizione dell'ottimizzazione. Ad esempio, è possibile decidere che si desidera solo creare indici su **table1**. A tale scopo, si elimina quindi la creazione delle viste indicizzate e il partizionamento da una indicazione relativa a un'ottimizzazione esistente. Ottimizzazione guidata motore di database crea una nuova sessione di ottimizzazione e ottimizza il carico di lavoro in rapporto ai database utilizzando le indicazioni modificate come configurazione ipotetica. Ciò significa che il carico di lavoro viene ottimizzato da Ottimizzazione guidata motore di database in rapporto ai database come se le indicazioni modificate fossero stati implementate, consentendo di eseguire analisi di simulazione limitate. È possibile eseguire solo analisi di simulazione limitate poiché l'utilizzo della GUI di Ottimizzazione guidata motore di database consente di scegliere solo un subset di una indicazione esistente. Per eseguire un'analisi di simulazione completa, specificando una configurazione ipotetica completamente nuova che non corrisponda a un subset di una sessione di ottimizzazione precedente, è necessario usare il file di input con estensione xml di Ottimizzazione guidata motore di database con l'utilità della riga di comando **dta** .  
  
##### <a name="to-evaluate-an-existing-tuning-session"></a>Per valutare una sessione di ottimizzazione esistente  
  
1.  Dopo l'avvio di Ottimizzazione guidata motore di database, fare doppio clic su una sessione di ottimizzazione nella parte superiore di **Monitoraggio sessione**, in modo da caricare le informazioni sulla sessione in Ottimizzazione guidata motore di database.  
  
2.  Selezionare la scheda **Stato** per controllare il log di ottimizzazione, che contiene informazioni sugli errori relativi a tutti gli eventi del carico di lavoro non ottimizzati da Ottimizzazione guidata motore di database. Tali informazioni possono contribuire alla valutazione dell'efficacia del carico di lavoro.  
  
3.  Per una ulteriore valutazione dei risultati dell'ottimizzazione di questa sessione, selezionare la scheda **Report** . Tale scheda consente di visualizzare il riepilogo dell'ottimizzazione o di selezionare un report di ottimizzazione nell'elenco **Selezionare il report** .  
  
4.  Selezionare la scheda **Indicazioni** per visualizzare le indicazioni relative all'ottimizzazione.  
  
5.  In caso di dubbi sull'implementazione di alcune indicazioni, deselezionarle.  
  
6.  Scegliere **Valuta indicazioni** dal menu **Azioni**. Ottimizzazione guidata motore di database crea una nuova sessione di ottimizzazione in cui le indicazioni modificate vengono utilizzate come configurazione ipotetica. Per visualizzare la configurazione ipotetica in formato XML, scegliere **Fare clic qui per vedere la sezione di configurazione**.  
  
7.  Nella scheda **Generale** immettere un **Nome sessione**e quindi assicurarsi che sia stato specificato il **Carico di lavoro** corretto.  
  
8.  Nella scheda **Opzioni di ottimizzazione** è possibile specificare un orario per l'ottimizzazione o definire le **Opzioni avanzate**disponibili.  
  
9. Fare clic sul pulsante **Avvia analisi** sulla barra degli strumenti. Ottimizzazione guidata motore di database avvia l'ottimizzazione dei database utilizzando la configurazione ipotetica. Al termine di Ottimizzazione guidata motore di database è possibile visualizzare i risultati della sessione in modo analogo ai risultati delle altre sessioni.  
  
### <a name="clone-existing-tuning-sessions"></a>Clonazione di sessioni di ottimizzazione esistenti  
 È possibile creare nuove sessioni di ottimizzazione basate su sessioni esistenti, scegliendo l'opzione relativa alla clonazione in Ottimizzazione guidata motore di database. Quando si utilizza tale opzione, si basa una nuova sessione di ottimizzazione su una sessione esistente. È quindi possibile modificare le opzioni di ottimizzazione per la nuova sessione in base alla necessità. Quando si valuta una sessione esistente come illustrato nella procedura precedente, Ottimizzazione guidata motore di database crea anche una nuova sessione di ottimizzazione, ma non è possibile modificare le opzioni di ottimizzazione.  
  
##### <a name="to-create-new-tuning-sessions-by-cloning-existing-sessions"></a>Per creare nuove sessioni di ottimizzazione clonando sessioni esistenti  
  
1.  Dopo l'avvio di Ottimizzazione guidata motore di database, fare doppio clic su una sessione di ottimizzazione nella parte superiore di **Monitoraggio sessione**, in modo da caricare le informazioni sulla sessione in Ottimizzazione guidata motore di database.  
  
2.  Scegliere **Clona sessione** dal menu **Azioni**.  
  
3.  Nella scheda **Generale** immettere un **Nome sessione**e quindi assicurarsi che sia stato specificato il **Carico di lavoro** corretto.  
  
4.  Nella scheda **Opzioni di ottimizzazione** è possibile specificare un orario per l'ottimizzazione, le strutture fisiche che potranno essere create da Ottimizzazione guidata motore di database e le indicazioni da eliminare.  
  
5.  Fare clic su **Opzioni avanzate** per impostare un limite di spazio per le indicazioni o un numero massimo di colonne per indice e per stabilire se si desidera che Ottimizzazione guidata motore di database generi indicazioni che possono essere implementate quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è online.  
  
6.  Fare clic sul pulsante **Avvia analisi** sulla barra degli strumenti per analizzare gli effetti del carico di lavoro in modo analogo alle altre sessioni di ottimizzazione. Al termine di Ottimizzazione guidata motore di database è possibile visualizzare i risultati della sessione in modo analogo ai risultati delle altre sessioni.  
  
##  <a name="UI"></a> Descrizioni dell'interfaccia utente  
  
### <a name="sessions-monitor"></a>Monitoraggio delle sessioni  
 **Monitoraggio sessione** consente di visualizzare informazioni sulle sessioni aperte in Ottimizzazione guidata motore di database. Selezionare un nome di sessione in **Monitoraggio sessione**per visualizzare informazioni sulla sessione nella finestra delle proprietà.  
  
### <a name="recommendations-tab"></a>Scheda Indicazioni  
 La scheda **Indicazioni** viene visualizzata al termine dell'analisi di un carico di lavoro da parte di Ottimizzazione guidata motore di database. Questa griglia contiene le indicazioni relative a ogni oggetto analizzato. Le indicazioni relative alle partizioni, se presenti, vengono visualizzate nella griglia superiore, mentre quelle relative agli indici vengono visualizzate nella griglia inferiore. Se non vi sono indicazioni, non viene visualizzata alcuna griglia.  
  
 La colonna **Definizione** contiene la definizione della partizione o dell'indice per cui sono presenti indicazioni in formato di collegamento ipertestuale. Questa colonna in genere non è sufficientemente ampia per visualizzare la definizione per intero. Fare clic sul collegamento ipertestuale per visualizzare una finestra di dialogo contenente la definizione completa e il pulsante **Copia negli Appunti** .  
  
#### <a name="partition-recommendations"></a>Indicazioni relative alle partizioni  
 **Nome database**  
 Database contenente gli oggetti che è consigliabile modificare.  
  
 **Consiglio**  
 Azione consigliata per migliorare le prestazioni. I valori possibili sono Crea ed Elimina.  
  
 **Destinazione indicazione**  
 Funzione o schema di partizione interessato dall'indicazione. L'icona visualizzata in questa colonna indica se è consigliabile eliminare o aggiungere la **Destinazione indicazione** e se si tratta di uno schema o di una funzione di partizione.  
  
 **Dettagli**  
 Descrizione di **Destinazione indicazione**. I valori possibili includono un intervallo per le funzioni di partizione o un valore vuoto per gli schemi di partizione.  
  
 **Numero partizioni**  
 Numero di partizioni definite dalle funzioni di partizione consigliate. Quando questa funzione viene utilizzata con un schema e quindi applicata a una tabella, i dati contenuti in tale tabella vengono divisi nel numero indicato di partizioni.  
  
 **Definizione**  
 Definizione di **Destinazione indicazione**. Fare clic sulla colonna per aprire la finestra di dialogo Anteprima script SQL, contenente uno script per l'azione consigliata.  
  
##### <a name="index-recommendations"></a>Indicazioni relative agli indici  
 **Database Name**  
 Database contenente gli oggetti che è consigliabile modificare.  
  
 **nome oggetto**  
 Tabella relativa all'indicazione.  
  
 **Consiglio**  
 Azione consigliata per migliorare le prestazioni. I valori possibili sono Crea ed Elimina.  
  
 **Destinazione indicazione**  
 Vista o indice interessato dall'indicazione. L'icona visualizzata in questa colonna indica se è consigliabile eliminare o aggiungere la **Destinazione indicazione**.  
  
 **Dettagli**  
 Descrizione di **Destinazione indicazione**. I valori possibili includono clustered, indexed view o vuoto, ovvero un indice non cluster. Viene inoltre indicato se l'indice è univoco.  
  
 **Schema partizione**  
 Se viene consigliato il partizionamento, in questa colonna viene visualizzato lo schema di partizione.  
  
 **Dimensioni (KB)**  
 Dimensioni previste del nuovo oggetto consigliato. Se la colonna è vuota, fare clic su **Fare clic su Report per visualizzare le dimensioni degli oggetti esistenti**.  
  
 **Definizione**  
 Definizione di **Destinazione indicazione**. Fare clic sulla colonna per aprire la finestra di dialogo Anteprima script SQL, contenente uno script per l'azione consigliata.  
  
 **Mostra oggetti esistenti**  
 Se selezionata, questa opzione consente di visualizzare tutti gli oggetti esistenti nella griglia, anche se Ottimizzazione guidata motore di database non ha espresso alcuna indicazione relativa agli oggetti.  
  
 **Fare clic su Report per visualizzare le dimensioni degli oggetti esistenti**  
 Selezionare questa opzione per visualizzare i report che indicano le dimensioni degli oggetti selezionati nella griglia delle indicazioni.  
  
### <a name="actions-menuapply-recommendations-options"></a>Menu Azioni/Opzioni di Applica indicazioni  
 Dopo l'analisi di un carico di lavoro e la generazione di indicazioni, scegliere **Applica indicazioni** dal menu **Azioni** per aprire la finestra di dialogo **Applica indicazioni** .  
  
 **Applica ora**  
 Consente di generare uno script per le indicazioni e di eseguirlo per implementare le indicazioni in questione.  
  
 **Pianifica per un momento successivo**  
 Consente di generare uno script per le indicazioni e di salvare le azioni come processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
 **Data**  
 Consente di specificare la data in cui si desidera eseguire il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'applicazione delle indicazioni.  
  
 **Time**  
 Consente di specificare l'ora in cui si desidera eseguire il processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per l'applicazione delle indicazioni.  
  
### <a name="reports-tab-options"></a>Opzioni della scheda Report  
 La scheda **Report** viene visualizzata quando l'Ottimizzazione guidata motore di database ha completato l'analisi di un carico di lavoro.  
  
 **Riepilogo ottimizzazione**  
 Consente di visualizzare un riepilogo delle indicazioni dell'Ottimizzazione guidata motore di database.  
  
 **Data**  
 Data di creazione del report da parte dell'Ottimizzazione guidata motore di database.  
  
 **Time**  
 Ora di creazione del report da parte dell'Ottimizzazione guidata motore di database.  
  
 **Server**  
 Server di destinazione del carico di lavoro dell'Ottimizzazione guidata motore di database.  
  
 **Database da ottimizzare**  
 Database al quale si riferiscono le indicazioni dell'Ottimizzazione guidata motore di database.  
  
 **File del carico di lavoro**  
 Questa opzione viene visualizzata se il carico di lavoro è un file.  
  
 **Tabella del carico di lavoro**  
 Questa opzione viene visualizzata se il carico di lavoro è una tabella di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Carico di lavoro**  
 Questa opzione viene visualizzata se il carico di lavoro è stato importato dall'editor di query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Tempo massimo per l'ottimizzazione**  
 Tempo massimo configurato che deve essere disponibile per l'analisi dell'Ottimizzazione guidata motore di database.  
  
 **Tempo impiegato per l'ottimizzazione**  
 Tempo effettivamente impiegato dall'Ottimizzazione guidata motore di database per analizzare il carico di lavoro.  
  
 **Miglioramento percentuale previsto**  
 Miglioramento percentuale previsto per il carico di lavoro definito che si ottiene implementando tutte le indicazioni dell'Ottimizzazione guidata motore di database.  
  
 **Spazio massimo per le indicazioni (MB)**  
 Spazio massimo previsto per le indicazioni. Questo valore viene configurato prima dell'esecuzione dell'analisi utilizzando il pulsante **Opzioni avanzate** nella scheda **Opzioni di ottimizzazione** .  
  
 **Spazio attualmente utilizzato (MB)**  
 Spazio attualmente utilizzato dagli indici nel database analizzato.  
  
 **Spazio utilizzato seguendo le indicazioni (MB)**  
 Spazio approssimativo che verrà utilizzato dagli indici implementando tutte le indicazioni dell'Ottimizzazione guidata motore di database.  
  
 **Numero di eventi nel carico di lavoro**  
 Numero di eventi contenuti nel carico di lavoro.  
  
 **Numero di eventi ottimizzati**  
 Numero di eventi ottimizzati nel carico di lavoro. Se un evento non può essere ottimizzato, viene elencato nel log di ottimizzazione, disponibile nella scheda **Stato** .  
  
 **Numero di istruzioni ottimizzate**  
 Numero di istruzioni ottimizzate nel carico di lavoro. Se un'istruzione non può essere ottimizzata, viene elencata nel log di ottimizzazione, disponibile nella scheda **Stato** .  
  
 **Percentuale di istruzioni SELECT nel set ottimizzato**  
 Percentuale di istruzioni SELECT ottimizzate. Questa opzione viene visualizzata solo in presenza di istruzioni SELECT ottimizzate.  
  
 **Percentuale di istruzioni UPDATE nel set ottimizzato**  
 Percentuale di istruzioni UPDATE ottimizzate. Questa opzione viene visualizzata solo in presenza di istruzioni UPDATE ottimizzate.  
  
 **Numero di indici che è consigliabile creare | eliminare**  
 Numero consigliato di indici da creare o eliminare nel database ottimizzato. Questa opzione viene visualizzata solo se gli indici fanno parte dell'indicazione.  
  
 **Numero di indici sulle viste che è consigliabile creare | eliminare**  
 Numero consigliato di indici sulle viste da creare o eliminare nel database ottimizzato. Questa opzione viene visualizzata solo se gli indici sulle viste fanno parte dell'indicazione.  
  
 **Numero di statistiche che è consigliabile creare**  
 Numero consigliato di statistiche da creare nel database ottimizzato. Questa opzione viene visualizzata solo se le statistiche fanno parte dell'indicazione.  
  
 **Select Report**  
 Consente di visualizzare i dettagli del report selezionato. Le colonne della griglia cambiano a seconda del report.  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e utilizzo di Ottimizzazione guidata motore di database](database-engine-tuning-advisor.md)   
 [Utilità dta](../../tools/dta/dta-utility.md)  
  
  
