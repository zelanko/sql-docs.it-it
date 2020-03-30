---
title: Query di Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d24d4e8bdebca82ec0541132b52ac84de6c9c271
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71284487"
---
# <a name="integration-services-ssis-queries"></a>Query di Integration Services (SSIS)

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  L'attività Esegui SQL, l'origine OLE DB, la destinazione OLE DB e la trasformazione Ricerca possono utilizzare query SQL. Nell'attività Esegui SQL, tramite le istruzioni SQL vengono creati, aggiornati ed eliminati dati e oggetti di database e vengono eseguite stored procedure e istruzioni SELECT. Nell'origine OLE DB e nella trasformazione Ricerca, le istruzioni SQL sono solitamente istruzioni SELECT o EXEC. Queste ultime eseguono in genere stored procedure che restituiscono set di risultati.  
  
 Le query possono essere analizzate per stabilire se sono valide. Quando si analizza una query che utilizza una connessione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la query viene analizzata ed eseguita e il risultato dell'esecuzione, ovvero esito positivo o negativo, viene assegnato al risultato dell'analisi. Se la query utilizza una connessione a dati diversi da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], l'istruzione viene semplicemente analizzata.  
  
È possibile specificare l'istruzione SQL nei modi seguenti:
1.   Immettendola direttamente nella finestra di progettazione.
2.   Specificando una connessione a un file che contiene l'istruzione.
3.   Specificando una variabile che contiene l'istruzione.  
  
## <a name="direct-input-sql"></a>SQL a input diretto  
 Generatore query è disponibile nell'interfaccia utente per l'attività Esegui SQL, l'origine OLE DB, la destinazione OLE DB e la trasformazione Ricerca. Tramite Generatore query è possibile:  
  
-   Lavorare in modo visivo o con comandi SQL.  
  
     Generatore query include riquadri grafici per la formulazione delle query in modo visivo e un riquadro di testo in cui viene visualizzato il testo SQL per la query. È possibile lavorare nei riquadri grafici o in quello di testo. Generatore query sincronizza i due tipi di visualizzazione affinché il testo della query e la rappresentazione grafica siano sempre corrispondenti.  
  
-   Unire in join tabelle correlate.  
  
     Se in una query si aggiungono più tabelle, Generatore query determina automaticamente il tipo di relazione tra le tabelle e formula il comando di join appropriato.  
  
-   Eseguire query o aggiornare database.  
  
     Tramite Generatore query è possibile restituire dati eseguendo istruzioni Transact-SQL SELECT oppure creare query per l'aggiornamento, l'aggiunta o l'eliminazione di record in un database.  
  
-   Visualizzare e modificare immediatamente i risultati.  
  
     È possibile eseguire una query e utilizzare un recordset in una griglia che consente di scorrere e modificare i record del database.  
  
 Sebbene Generatore query consenta di creare solamente query SELECT in modo visivo, nel riquadro di testo è possibile digitare il codice SQL per altri tipi di istruzioni, ad esempio DELETE e UPDATE. Il riquadro grafico viene aggiornato automaticamente in base all'istruzione SQL digitata.  
  
 È inoltre possibile fornire input diretto digitando la query nella finestra di dialogo dell'attività o del componente del flusso di dati oppure nella finestra Proprietà.  
  
 Per altre informazioni, vedere [Generatore di query](https://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5).  
  
## <a name="sql-in-files"></a>SQL nei file  
 L'istruzione SQL dell'attività Esegui SQL può essere inclusa inoltre in un file distinto. È possibile, ad esempio, scrivere query utilizzando strumenti quali l'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], salvare la query in un file e quindi leggere la query dal file durante l'esecuzione di un pacchetto. Il file può contenere soltanto le istruzioni SQL da eseguire e commenti. Per eseguire un'istruzione SQL archiviata in un file, è necessario fornire una connessione file che specifica il nome e la posizione del file. Per altre informazioni, vedere [File Connection Manager](../integration-services/connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL nelle variabili  
 Se l'origine dell'istruzione SQL nell'attività Esegui SQL è una variabile, è necessario specificare il nome delle variabile contenente la query. Il testo della query è specificato nella proprietà Value della variabile. È necessario impostare la proprietà ValueType della variabile su un tipo di dati string e quindi digitare o copiare l'istruzione SQL nella proprietà Value. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787).  

## <a name="query-builder-dialog-box"></a>Generatore query - finestra di dialogo
Utilizzare la finestra di dialogo **Generatore query** per creare una query da utilizzare nell'attività Esegui SQL, nell'origine e nella destinazione OLE DB, nonché nella trasformazione Ricerca.  
  
 È possibile utilizzare Generatore query per eseguire le attività seguenti:  
  
-   **Utilizzare la rappresentazione grafica di una query o comandi SQL** Generatore query include un riquadro che contiene una rappresentazione grafica della query e un riquadro in cui viene visualizzato il testo SQL della query. È possibile utilizzare indifferentemente il riquadro del grafico o il riquadro del testo. Generatore query sincronizza le visualizzazioni in modo che siano sempre aggiornate.  
  
-   **Unire in join tabelle correlate** Se in una query si aggiungono più tabelle, Generatore query determina automaticamente il tipo di relazione tra le tabelle e formula il comando di join appropriato.  
  
-   **Aggiornare o eseguire query di database** È possibile usare Generatore query per restituire dati usando istruzioni Transact-SQL di tipo SELECT e creare query per l'aggiornamento, l'inserimento e l'eliminazione di record in un database.  
  
-   **Visualizzare e modificare immediatamente i risultati** È possibile eseguire una query ed eseguire operazioni su un recordset in una griglia che consente di scorrere e modificare i record nel database.  
  
 Gli strumenti grafici inclusi nella finestra di dialogo **Generatore query** consentono di costruire query mediante operazioni di trascinamento. Per impostazione predefinita, la finestra di dialogo Generatore query consente di compilare query SELECT, ma è possibile creare anche query INSERT, UPDATE o DELETE. Nella finestra di dialogo **Generatore query** è inoltre possibile analizzare ed eseguire tutti i tipi di istruzioni SQL. Per altre informazioni sulle istruzioni SQL nei pacchetti, vedere [Query di Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-queries.md).  
  
 Per sapere di più sul linguaggio di query Transact-SQL e la relativa sintassi, vedere [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](../t-sql/transact-sql-reference-database-engine.md).  
  
 È inoltre possibile utilizzare variabili in una query per specificare i valori per un parametro di input, acquisire i valori dei parametri di output e memorizzare i codici restituiti. Per sapere di più sull'uso delle variabili nelle query usate dai pacchetti, vedere [Attività Esegui SQL](../integration-services/control-flow/execute-sql-task.md), [Origine OLE DB](../integration-services/data-flow/ole-db-source.md)e [Integration Services &#40;SSIS&#41; Queries](../integration-services/integration-services-ssis-queries.md). Per sapere di più sull'uso delle variabili nell'attività Esegui SQL, vedere [Parametri e codici restituiti nell'attività Esegui SQL](https://msdn.microsoft.com/library/a3ca65e8-65cf-4272-9a81-765a706b8663) e [Set di risultati nell'attività Esegui SQL](https://msdn.microsoft.com/library/62605b63-d43b-49e8-a863-e154011e6109).  
  
 Anche nelle trasformazioni Ricerca e Ricerca fuzzy è possibile utilizzare le variabili con parametri e codici restituiti. Le informazioni relative all'origine OLE DB si applicano anche a queste due trasformazioni.  
  
### <a name="options"></a>Opzioni  
 **Barra degli strumenti**  
 Utilizzare la barra degli strumenti per gestire set di dati, selezionare i riquadri da visualizzare e controllare le funzioni di query.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Mostra/Nascondi riquadro diagramma**|Consente di visualizzare o nascondere il riquadro **diagramma**.|  
|**Mostra/Nascondi riquadro griglia**|Consente di visualizzare o nascondere il riquadro **griglia**.|  
|**Mostra/Nascondi riquadro SQL**|Consente di visualizzare o nascondere il riquadro **SQL**.|  
|**Mostra/Nascondi riquadro Risultati**|Consente di visualizzare o nascondere il riquadro dei **risultati**.|  
|**Esegui**|Consente di eseguire la query. I risultati verranno visualizzati nel riquadro dei risultati.|  
|**Verifica istruzione SQL**|Consente di verificare che l'istruzione sia valida.|  
|**Ordinamento crescente**|Consente di disporre in ordine crescente le righe di output della colonna selezionata nel riquadro griglia.|  
|**Ordinamento decrescente**|Consente di disporre in ordine decrescente le righe di output della colonna selezionata nel riquadro griglia.|  
|**Rimuovi filtro**|Selezionare un nome di colonna nel riquadro griglia e quindi fare clic su **Rimuovi filtro** per rimuovere i criteri di ordinamento per la colonna.|  
|**Usa Group By**|Consente di aggiungere funzionalità di raggruppamento GROUP BY alla query.|  
|**Aggiungi tabella**|Consente di aggiungere una nuova tabella alla query.|  
  
 **Definizione query**  
 Questa opzione mette a disposizione una barra degli strumenti e riquadri in cui è possibile definire e testare la query.  
  
|Riquadro|Descrizione|  
|----------|-----------------|  
|**Riquadro diagramma**|Visualizza la query in un diagramma. Nel diagramma vengono visualizzate le tabelle incluse nella query e indicate le relative modalità di unione in join. Selezionare o deselezionare la casella di controllo accanto a una colonna nella tabella per aggiungere o rimuovere la colonna dall'output della query.<br /><br /> Quando si aggiungono tabelle alla query, in Generatore query vengono creati join tra le tabelle basati sulle tabelle, in base alle chiavi della tabella. Per aggiungere un join, trascinare un campo da una tabella in un campo di un'altra tabella. Per gestire un join, fare clic su di esso con il pulsante destro del mouse e quindi scegliere un'opzione dal menu.<br /><br /> Fare clic con il pulsante destro del mouse sul riquadro **Diagramma** per aggiungere o rimuovere tabelle, selezionare tutte le tabelle e visualizzare o nascondere i riquadri.|  
|**Riquadro griglia**|Visualizza la query in una griglia. È possibile utilizzare questo riquadro per aggiungere o rimuovere colonne da un query e modificare le impostazioni per ogni colonna.|  
|**Riquadro SQL**|Visualizza la query come testo di istruzione SQL. Le modifiche apportate nei riquadri **diagramma** e **griglia** vengono visualizzati qui e viceversa, le modifiche apportate qui vengono visualizzate nei riquadri **diagramma** e **griglia**.|  
|Riquadro**Risultati**|Visualizza i risultati della query quando si fa clic su **Esegui** sulla barra degli strumenti.| 

  
