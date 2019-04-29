---
title: Generatore di query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.querybuilder.f1
helpviewer_keywords:
- Query Builder dialog box
ms.assetid: 780752c9-6e3c-4f44-aaff-4f4d5e5a45c5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e09e41535ad878a3f20ae74df07ace7bda6fa7e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62889584"
---
# <a name="query-builder"></a>Generatore di query
  Utilizzare la finestra di dialogo **Generatore query** per creare una query da utilizzare nell'attività Esegui SQL, nell'origine e nella destinazione OLE DB, nonché nella trasformazione Ricerca.  
  
 È possibile utilizzare Generatore query per eseguire le attività seguenti:  
  
-   **Utilizzare la rappresentazione grafica di una query o comandi SQL** Generatore query include un riquadro che contiene una rappresentazione grafica della query e un riquadro in cui viene visualizzato il testo SQL della query. È possibile utilizzare indifferentemente il riquadro del grafico o il riquadro del testo. Generatore query sincronizza le visualizzazioni in modo che siano sempre aggiornate.  
  
-   **Unire in join tabelle correlate** Se in una query si aggiungono più tabelle, Generatore query determina automaticamente il tipo di relazione tra le tabelle e formula il comando di join appropriato.  
  
-   **Aggiornare o eseguire query di database** È possibile usare Generatore query per restituire dati usando istruzioni Transact-SQL di tipo SELECT e creare query per l'aggiornamento, l'inserimento e l'eliminazione di record in un database.  
  
-   **Visualizzare e modificare immediatamente i risultati** È possibile eseguire una query ed eseguire operazioni su un recordset in una griglia che consente di scorrere e modificare i record nel database.  
  
 Gli strumenti grafici inclusi nella finestra di dialogo **Generatore query** consentono di costruire query mediante operazioni di trascinamento. Per impostazione predefinita, la finestra di dialogo Generatore query consente di compilare query SELECT, ma è possibile creare anche query INSERT, UPDATE o DELETE. Nella finestra di dialogo **Generatore query** è inoltre possibile analizzare ed eseguire tutti i tipi di istruzioni SQL. Per altre informazioni sulle istruzioni SQL nei pacchetti, vedere [Query di Integration Services &#40;SSIS&#41;](integration-services-ssis-queries.md).  
  
 Per sapere di più sul linguaggio di query Transact-SQL e la relativa sintassi, vedere [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](/sql/t-sql/language-reference).  
  
 È inoltre possibile utilizzare variabili in una query per specificare i valori per un parametro di input, acquisire i valori dei parametri di output e memorizzare i codici restituiti. Per sapere di più sull'uso delle variabili nelle query usate dai pacchetti, vedere [Attività Esegui SQL](control-flow/execute-sql-task.md), [Origine OLE DB](data-flow/ole-db-source.md)e [Integration Services &#40;SSIS&#41; Queries](integration-services-ssis-queries.md). Per sapere di più sull'uso delle variabili nell'attività Esegui SQL, vedere [Parametri e codici restituiti nell'attività Esegui SQL](../../2014/integration-services/parameters-and-return-codes-in-the-execute-sql-task.md) e [Set di risultati nell'attività Esegui SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md).  
  
 Anche nelle trasformazioni Ricerca e Ricerca fuzzy è possibile utilizzare le variabili con parametri e codici restituiti. Le informazioni relative all'origine OLE DB si applicano anche a queste due trasformazioni.  
  
## <a name="options"></a>Opzioni  
 **Barra degli strumenti**  
 Utilizzare la barra degli strumenti per gestire set di dati, selezionare i riquadri da visualizzare e controllare le funzioni di query.  
  
|Value|Descrizione|  
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
|Riquadro**Risultati** |Visualizza i risultati della query quando si fa clic su **Esegui** sulla barra degli strumenti.|  
  
## <a name="see-also"></a>Vedere anche  
 [Attività Esegui SQL](control-flow/execute-sql-task.md)   
 [Origine OLE DB](data-flow/ole-db-source.md)   
 [Destinazione OLE DB](data-flow/ole-db-destination.md)   
 [Trasformazione Ricerca](data-flow/transformations/lookup-transformation.md)   
 [Integration Services &#40;SSIS&#41; le query](integration-services-ssis-queries.md)   
 [MERGE nei pacchetti di Integration Services](control-flow/merge-in-integration-services-packages.md)  
  
  
