---
title: Usare l'Editor Transact-SQL per modificare ed eseguire script | Microsoft Docs
ms.custom:
- SSDT
ms.date: 02/09/2017
ms.prod: sql
ms.technology: ssdt
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- SQL.DATA.TOOLS.SQLEDITOR
ms.assetid: fa78e2cf-3c64-49f5-93cc-a3d50b1e7d05
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 2c2b84cb9f75987995e9e0cdbf92165fa28f61a9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68006036"
---
# <a name="use-transact-sql-editor-to-edit-and-execute-scripts"></a>Utilizzare l'Editor Transact-SQL per modificare ed eseguire script
L'editor Transact\-SQL offre un'esperienza di modifica e di debug completa durante l'utilizzo degli script. Viene richiamato quando si usa il menu contestuale **Visualizza codice** per aprire un'entità del database in un progetto o in un database connesso. Viene anche aperto automaticamente quando si usa il menu contestuale **Nuova query** da Esplora oggetti di SQL Server o si aggiunge un nuovo oggetto script a un progetto di database.  
  
Se non si è connessi a un database ma si vuole eseguire una query sul database stesso, è anche possibile usare la finestra di dialogo **Nuova connessione query** nell'opzione di menu **SQL** -> **Editor Transact\-SQL** per connettersi a un database e avviare l'editor Transact\-SQL.  
  
Nell'editor Transact\-SQL è disponibile un riquadro **T-SQL** principale in cui è possibile scrivere e modificare script Transact\-SQL. L'editor supporta IntelliSense e il codice a colori della sintassi per migliorare la leggibilità di istruzioni complesse. Supporta inoltre le operazioni di ricerca e sostituzione, creazione di commenti bulk, caratteri e colori personalizzati e numerazione delle righe. Inoltre, è possibile modificare il database in cui sarà eseguito lo script nell'editor. Per altre informazioni, vedere [Procedura: Clonare un database esistente](../ssdt/how-to-clone-an-existing-database.md). Nel riquadro **Risultati** vengono visualizzati i risultati della query in una griglia o in un testo. Tali risultati possono anche essere reindirizzati in un file. Nel riquadro **Messaggio** vengono visualizzati errori, avvisi e messaggi informativi restituiti quando viene eseguito uno script. Se le statistiche client sono abilitate, nel riquadro **Statistiche** vengono visualizzate le informazioni sull'esecuzione di query raggruppate in categorie. Nel riquadro **Piano di esecuzione** vengono visualizzati i metodi di recupero dei dati scelti da SQL Server e vengono mostrati i costi di esecuzione di istruzioni e query specifiche.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
|Argomento|Descrizione|  
|---------|---------------|  
|[Procedura: Strutturare e aggiungere frammenti di codice allo script Transact-SQL](../ssdt/how-to-outline-and-add-snippets-to-transact-sql-script.md)|Usare Selezione frammento di codice per inserire il codice Transact\-SQL pronto nella query.|  
|[Procedura: Navigare tra script](../ssdt/how-to-navigate-between-scripts.md)|Utilizzare Vai a definizione e Trova tutti i riferimenti per navigare tra gli script.|  
|[Procedura: Usare la ridenominazione e il refactoring per apportare modifiche agli oggetti di database](../ssdt/how-to-use-rename-and-refactoring-to-make-changes-to-your-database-objects.md)|Rinominare un oggetto in tutti gli script e visualizzare tutte le modifiche in anteprima.|  
|[Procedura: Eseguire una query parziale](../ssdt/how-to-execute-a-partial-query.md)|Evidenziare un segmento specifico dello script ed eseguirlo come una singola query.|  
|[Procedura: Eseguire il debug di stored procedure](../ssdt/how-to-debug-stored-procedures.md)|Creare ed eseguire il debug di una stored procedure Transact\-SQL eseguendo le singole istruzioni.|  
|[Analizzare le prestazioni degli script](../ssdt/analyze-script-performance.md)|Utilizzare piani di esecuzione, statistiche client e analisi codice per determinare se è possibile migliorare le prestazioni di query, stored procedure o script.|  
  
## <a name="see-also"></a>Vedere anche  
[Procedura: Creare nuovi oggetti di database tramite query](../ssdt/how-to-create-new-database-objects-using-queries.md)  
  
