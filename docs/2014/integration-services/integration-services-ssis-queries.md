---
title: Query di Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Query Builder [Integration Services]
- queries [Integration Services]
- statements [Integration Services]
- queries [Integration Services], about queries in packages
ms.assetid: 8822bd29-4575-46c8-92a0-1a39bc2604c1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 5ea5de1e9dacd6cce5c4e0b199d7220413da06d7
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85436288"
---
# <a name="integration-services-ssis-queries"></a>Query di Integration Services (SSIS)
  L'attività Esegui SQL, l'origine OLE DB, la destinazione OLE DB e la trasformazione Ricerca possono utilizzare query SQL. Nell'attività Esegui SQL, tramite le istruzioni SQL vengono creati, aggiornati ed eliminati dati e oggetti di database e vengono eseguite stored procedure e istruzioni SELECT. Nell'origine OLE DB e nella trasformazione Ricerca, le istruzioni SQL sono solitamente istruzioni SELECT o EXEC. Queste ultime eseguono in genere stored procedure che restituiscono set di risultati.  
  
 Le query possono essere analizzate per stabilire se sono valide. Quando si analizza una query che utilizza una connessione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], la query viene analizzata ed eseguita e il risultato dell'esecuzione, ovvero esito positivo o negativo, viene assegnato al risultato dell'analisi. Se la query utilizza una connessione a dati diversi da [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], l'istruzione viene semplicemente analizzata.  
  
 È possibile definire l'istruzione SQL immettendola direttamente nella finestra di progettazione oppure specificando una connessione file o una variabile contenente l'istruzione.  
  
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
  
 Per altre informazioni, vedere [Generatore di query](../../2014/integration-services/query-builder.md).  
  
## <a name="sql-in-files"></a>SQL nei file  
 L'istruzione SQL dell'attività Esegui SQL può essere inclusa inoltre in un file distinto. È possibile, ad esempio, scrivere query utilizzando strumenti quali l'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], salvare la query in un file e quindi leggere la query dal file durante l'esecuzione di un pacchetto. Il file può contenere soltanto le istruzioni SQL da eseguire e commenti. Per eseguire un'istruzione SQL archiviata in un file, è necessario fornire una connessione file che specifica il nome e la posizione del file. Per altre informazioni, vedere [File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="sql-in-variables"></a>SQL nelle variabili  
 Se l'origine dell'istruzione SQL nell'attività Esegui SQL è una variabile, è necessario specificare il nome delle variabile contenente la query. Il testo della query è specificato nella proprietà Value della variabile. È necessario impostare la proprietà ValueType della variabile su un tipo di dati string e quindi digitare o copiare l'istruzione SQL nella proprietà Value. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md) e [Utilizzo di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md).  
  
  
