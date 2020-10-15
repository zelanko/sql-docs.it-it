---
title: Interfaccia utente della finestra Progettazione query con interfaccia grafica | Microsoft Docs
description: Informazioni sull'interfaccia utente della finestra Progettazione query con interfaccia grafica, che consente di recuperare dati da un database relazionale per un set di dati del report in Progettazione report.
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
f1_keywords:
- "10012"
- sql13.rtp.rptdesigner.dataview.vdtquerydesigner.f1
helpviewer_keywords:
- graphical query designer [Reporting Services]
- data sources [Reporting Services], creating
- text-based query designer [Reporting Services]
- query designers [Reporting Services]
- Reporting Services, query designers
ms.assetid: 5022ae33-03a3-48de-8ac1-82742f48cebe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2f26eb4e27649e1b47af909f34fd2df6db61b904
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891311"
---
# <a name="graphical-query-designer-user-interface"></a>Interfaccia utente della finestra Progettazione query con interfaccia grafica
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] dispone di due finestre Progettazione query, una con interfaccia grafica e una basata su testo, per la creazione di query che consentano di recuperare i dati da un database relazionale per un set di dati del report in Progettazione report. Usare la finestra Progettazione query con interfaccia grafica per compilare in modo interattivo una query e visualizzare i risultati per origine dati di tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, OLE DB e ODBC. Usare la finestra Progettazione query basata su testo per specificare più istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] , la sintassi di una query complessa o del comando, nonché query basate su espressioni. Per altre informazioni, vedere [Interfaccia utente di Progettazione query basata su testo](/previous-versions/sql/). Per altre informazioni sull'uso di specifici tipi di origine dati, vedere [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md).  
  
 .  
  
## <a name="graphical-query-designer"></a>Finestra Progettazione query con interfaccia grafica  
 La finestra Progettazione query con interfaccia grafica supporta tre tipi di comandi di query: **Text**, **StoredProcedure** o **TableDirect**. Prima di creare una query per il set di dati, è necessario selezionare l'opzione del tipo di comando nella pagina Query della finestra di dialogo [Proprietà set di dati](/previous-versions/sql/) .  
  
 Sono disponibili le opzioni seguenti per tipo di query:  
  
-   **Text** Supporta il testo delle query [!INCLUDE[tsql](../../includes/tsql-md.md)] standard per le origini dati dei database relazionali, incluse le estensioni per l'elaborazione dati per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e Oracle.  
  
-   **TableDirect** Seleziona tutte le colonne della tabella specificata. Per una tabella denominata Customers, ad esempio, è l'equivalente dell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)]`SELECT * FROM Customers`.  
  
-   **StoredProcedure** Supporta chiamate a stored procedure nell'origine dei dati. Per utilizzare questa opzione è necessario che l'amministratore del database sull'origine dati abbia concesso le autorizzazioni di esecuzione sulla stored procedure.  
  
 Il tipo di comando predefinito è **Text**.  
  
> [!NOTE]  
>  Non tutte le estensioni per l'elaborazione dati supportano tutti i tipi. Il provider di dati sottostante deve supportare un tipo di comando affinché l'opzione sia disponibile.  
  
### <a name="command-type-text"></a>Tipo di comando Text  
 Nel tipo **Text** nella finestra Progettazione query con interfaccia grafica sono presenti quattro aree, o riquadri. È possibile specificare colonne, alias, valori di ordinamento e valori di filtro per una query [!INCLUDE[tsql](../../includes/tsql-md.md)] . È possibile visualizzare il testo della query generata dalle selezioni eseguite, eseguire la query e visualizzare il set di risultati. Nella figura seguente vengono illustrati i quattro riquadri.  
  
 ![Finestra Progettazione query con interfaccia grafica per query SQL](../../reporting-services/report-data/media/rsqd-dsaw-sql.gif "Finestra Progettazione query con interfaccia grafica per query SQL")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Diagramma|Consente di visualizzare le rappresentazioni grafiche delle tabelle nella query. Utilizzare questo riquadro per selezionare i campi e definire le relazioni tra le tabelle.|  
|Griglia|Consente di visualizzare un elenco dei campi restituiti dalla query. Utilizzare questo riquadro per definire gli alias, i valori di ordinamento, i filtri, i gruppi e i parametri.|  
|SQL|Consente di visualizzare la query [!INCLUDE[tsql](../../includes/tsql-md.md)] rappresentata nei riquadri diagramma e griglia. Usare questo riquadro per scrivere o aggiornare una query tramite [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|Risultato|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
 Le eventuali modifiche alle informazioni in uno dei primi tre riquadri vengono visualizzate negli altri. Se ad esempio si aggiunge una tabella nel riquadro diagramma, la tabella verrà automaticamente aggiunta alla query [!INCLUDE[tsql](../../includes/tsql-md.md)] nel riquadro SQL. Se si aggiunge un campo alla query nel riquadro SQL, il campo verrà automaticamente aggiunto all'elenco nel riquadro griglia e la tabella nel riquadro diagramma verrà aggiornata.  
  
 Per altre informazioni, vedere [Strumenti di progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md).  
  
#### <a name="toolbar-for-the-graphical-query-designer"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica  
 La barra degli strumenti per la finestra Progettazione query con interfaccia grafica include i pulsanti necessari per creare le query [!INCLUDE[tsql](../../includes/tsql-md.md)] tramite tale interfaccia.  
  
|Pulsante|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati solo i file con estensione sql e rdl. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Pulsante Mostra/Nascondi riquadro diagramma](../../reporting-services/report-data/media/rsqdicon-showhidediagram.gif "Pulsante Mostra/Nascondi riquadro diagramma")|Consente di visualizzare o nascondere il riquadro diagramma.|  
|![Pulsante Mostra/Nascondi riquadro griglia](../../reporting-services/report-data/media/rsqdicon-showhidegrid.gif "Pulsante Mostra/Nascondi riquadro griglia")|Consente di visualizzare o nascondere il riquadro griglia.|  
|![Pulsante Mostra/Nascondi riquadro SQL](../../reporting-services/report-data/media/rsqdicon-showhidesql.gif "Pulsante Mostra/Nascondi riquadro SQL")|Consente di visualizzare o nascondere il riquadro SQL.|  
|![Pulsante Mostra/Nascondi riquadro risultati](../../reporting-services/report-data/media/rsqdicon-showhideresult.gif "Pulsante Mostra/Nascondi riquadro risultati")|Consente di visualizzare o nascondere il riquadro risultati.|  
|![Eseguire la query](../../reporting-services/report-data/media/rsqdicon-run.gif "Eseguire la query")|Consente di eseguire la query.|  
|![Pulsante Verifica istruzione SQL nel riquadro SQL](../../reporting-services/report-data/media/rsqdicon-verifysql.gif "Pulsante Verifica istruzione SQL nel riquadro SQL")|Consente di verificare la correttezza della sintassi del testo della query.|  
|![Impostazione dell'ordinamento crescente per il campo selezionato](../../reporting-services/report-data/media/rsqdicon-sortascending.gif "Impostazione dell'ordinamento crescente per il campo selezionato")|Consente di impostare l'ordinamento su **Ordinamento crescente** per la colonna selezionata nel riquadro Diagramma,|  
|![Impostazione dell'ordinamento decrescente per il campo selezionato](../../reporting-services/report-data/media/rsqdicon-sortdescending.gif "Impostazione dell'ordinamento decrescente per il campo selezionato")|Consente di impostare l'ordinamento su **Ordinamento decrescente** per la colonna selezionata nel riquadro Diagramma,|  
|![Rimozione del filtro dal campo selezionato](../../reporting-services/report-data/media/rsqdicon-removefilter.gif "Rimozione del filtro dal campo selezionato")|Rimuovere il filtro per la colonna selezionata nel riquadro Diagramma contrassegnata come filtrata (![icona del filtro accanto alla colonna di filtro selezionata](../../reporting-services/report-data/media/rsqdicon-filter.gif "Icona del filtro accanto alla colonna di filtro selezionata")).|  
|![Usa "Group By" per il campo selezionato](../../reporting-services/report-data/media/rsqdicon-usegroupby.gif "Usa "Group By" per il campo selezionato")|Consente di visualizzare o nascondere la colonna **Group By** nel riquadro Griglia. Quando il pulsante Mostra/Nascondi **Group By** è attivo, una colonna aggiuntiva denominata **Group By** viene visualizzata nel riquadro Griglia e ogni valore per le colonne selezionate nella query viene impostato per impostazione predefinita su **Group By**. Questo determina l'inclusione della colonna selezionata in una clausola Group By nel testo SQL. Utilizzare il pulsante Group By per aggiungere automaticamente una clausola GROUP BY che include tutte le colonne nella clausola SELECT. Quando la clausola SELECT include chiamate di funzione aggregate, ad esempio SUM(ColumnName), includere ogni colonna non aggregata nella clausola GROUP BY per fare in modo che venga visualizzata nel set di risultati.<br /><br /> Per essere visualizzata nel riquadro risultati, è necessario che per ogni colonna della query sia definita una funzione aggregata da utilizzare nel calcolo del valore da visualizzare nel riquadro risultati, oppure che la colonna della query venga specificata nella clausola GROUP BY della query SQL.|  
|![Aggiunta di una nuova tabella al riquadro diagramma](../../reporting-services/report-data/media/rsqdicon-addtable.gif "Aggiunta di una nuova tabella al riquadro diagramma")|Consente di aggiungere una nuova tabella dall'origine dei dati nel riquadro diagramma.<br /><br /> **Note** Quando si aggiunge una nuova tabella, Progettazione query tenta di abbinare le relazioni di chiave esterna dell'origine dati. Dopo aver aggiunto una tabella, verificare che le relazioni di chiave esterna rappresentate dai collegamenti tra le tabelle siano corrette.|  
  
#### <a name="example"></a>Esempio  
 La query seguente restituisce l'elenco dei cognomi dalla tabella [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] Person **del database** :  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 È inoltre possibile eseguire stored procedure dal riquadro SQL. La query seguente esegue la stored procedure **uspGetEmployeeManagers** nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] :  
  
```  
EXEC uspGetEmployeeManagers '1';  
```  
  
### <a name="command-type-tabledirect"></a>Tipo di comando TableDirect  
 Nel tipo **TableDirect** nella finestra Progettazione query con interfaccia grafica viene visualizzato un elenco a discesa delle tabelle disponibili dall'origine dei dati e un riquadro Risultati. Se si seleziona una tabella e si fa clic sul pulsante **Esegui** , vengono restituite tutte le colonne per tale tabella.  
  
> [!NOTE]  
>  La caratteristica TableDirect è supportata solo dai tipi di origine dati **OLE DB** e **ODBC** .  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Elenco a discesa Tabella|Elenca tutte le tabelle disponibili dall'origine dei dati. Selezionare una stored procedure dall'elenco per attivarla.|  
|Risultato|Consente di visualizzare tutte le colonne dalla tabella selezionata. Per eseguire la query di tabella, fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="toolbar-buttons-for-the-command-type-tabledirect"></a>Pulsanti della barra degli strumenti per il tipo di comando TableDirect  
 La barra degli strumenti della finestra Progettazione query con interfaccia grafica include un elenco a discesa di tabelle nell'origine dei dati. Nella tabella seguente sono elencati tutti i pulsanti con le rispettive funzioni.  
  
|Pulsante|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati solo i file con estensione sql e rdl. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Icona del pulsante Progettazione query standard](../../reporting-services/report-data/media/icongenericquerydesigner.gif "Icona del pulsante Progettazione query standard")|Consente di passare dall'interfaccia di Progettazione query generica all'interfaccia grafica e viceversa, mantenendo la visualizzazione del testo della query o della stored procedure.|  
|![Eseguire la query](../../reporting-services/report-data/media/rsqdicon-run.gif "Eseguire la query")|Consente di selezione tutte le colonne della tabella selezionata.|  
  
### <a name="command-type-storedprocedure"></a>Tipo di comando StoredProcedure  
 Nel tipo **StoredProcedure** nella finestra Progettazione query con interfaccia grafica viene visualizzato un elenco a discesa delle stored procedure disponibili dall'origine dei dati e un riquadro Risultati. Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Elenco a discesa Stored procedure|Elenca tutte le stored procedure disponibili dall'origine dei dati. Selezionare una stored procedure dall'elenco per attivarla.|  
|Risultato|Consente di visualizzare il risultato dell'esecuzione della stored procedure. Per eseguire la stored procedure selezionata, fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="toolbar-buttons-for-command-type-storedprocedure"></a>Pulsanti della barra degli strumenti per il tipo di comando StoredProcedure  
 La barra degli strumenti della finestra Progettazione query con interfaccia grafica include un elenco a discesa di stored procedure sull'origine dei dati. Nella tabella seguente sono elencati tutti i pulsanti con le rispettive funzioni.  
  
|Pulsante|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati solo i file con estensione sql e rdl. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Eseguire la query](../../reporting-services/report-data/media/rsqdicon-run.gif "Eseguire la query")|Consente di eseguire la stored procedure selezionata.|  
|Elenco a discesa Stored procedure|Fare clic sulla freccia GIÙ per visualizzare un elenco delle stored procedure disponibili dall'origine dei dati. Fare clic su una stored procedure nell'elenco per selezionarla.|  
  
#### <a name="example"></a>Esempio  
 La stored procedure seguente chiama un elenco sotto forma di struttura gerarchica dei responsabili dal database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Questa stored procedure accetta *BusinessEntityID* come parametro. È possibile immettere qualsiasi integer di piccole dimensioni.  
  
 `uspGetEmployeeManagers '1';`  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di progettazione query &#40;SSRS&#41;](../../reporting-services/report-data/query-design-tools-ssrs.md)   
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Tipo di connessione SQL Server &#40;SSRS&#41;](../../reporting-services/report-data/sql-server-connection-type-ssrs.md)   
 [Tipo di connessione OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md)   
 [Set di dati del report &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)   
 [Tipo di connessione Oracle &#40;SSRS&#41;](../../reporting-services/report-data/oracle-connection-type-ssrs.md)   
 [RSReportDesigner - file di configurazione](../../reporting-services/report-server/rsreportdesigner-configuration-file.md)   
 [Procedure per la progettazione di query e viste &#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
