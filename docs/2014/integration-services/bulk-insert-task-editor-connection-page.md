---
title: Editor attività Inserimento bulk (pagina connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.bulkinserttask.connection.f1
helpviewer_keywords:
- Bulk Insert Task Editor
ms.assetid: 51252c20-8865-4ede-a3fd-bd73a968f47d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b6834a2a4cd75e70de253419cc42ec5904ce0793
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061215"
---
# <a name="bulk-insert-task-editor-connection-page"></a>Editor attività Inserimento bulk (pagina Connessione)
  Usare la pagina **Connessione** della finestra di dialogo **Editor attività Inserimento bulk** per specificare l'origine e la destinazione dell'operazione di inserimento bulk e il formato da usare.  
  
 Per altre informazioni sulle operazioni di inserimento bulk, vedere [Attività Inserimento bulk](control-flow/bulk-insert-task.md) e [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 **Connessione**  
 Selezionare una gestione connessione OLE DB nell'elenco o fare clic su \<**Nuova connessione...**> per creare una nuova connessione.  
  
 **Argomenti correlati:** [gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md), [configurazione OLE DB gestione connessione](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **DestinationTable**  
 Consente di digitare il nome della tabella o della vista di destinazione o di selezionare una tabella o una vista nell'elenco.  
  
 **Formato**  
 Consente di selezionare l'origine del formato per l'inserimento bulk. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Usa file**|Consente di selezionare un file contenente la specifica di formato. Selezionando questa opzione viene visualizzata l'opzione dinamica **FormatFile**.|  
|**Specificare**|Consente di specificare il formato. Selezionando questa opzione vengono visualizzate le opzioni `RowDelimiter` dinamiche `ColumnDelimiter`e.|  
  
 **File**  
 Selezionare una gestione connessione file o file flat nell'elenco oppure fare clic su \<**Nuova connessione...**> per creare una nuova connessione.  
  
 Il percorso del file è relativo al Motore di database di SQL Server specificato nella gestione connessione per questa attività. Il file di testo deve essere accessibile dal Motore di database di SQL Server in un disco rigido locale sul server oppure tramite un'unità condivisa o di cui è stato eseguito il mapping a SQL Server. Non è possibile accedere al file tramite SSIS Runtime.  
  
 Se si accede al file di origine utilizzando una gestione connessione file flat, l'attività Inserimento bulk non utilizzerà il formato specificato nella gestione connessione file flat, ma userà il formato specificato in un file di formato o i valori delle proprietà RowDelimiter e ColumnDelimiter dell'attività.  
  
 **Argomenti correlati:** [gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md), [gestione connessione file](connection-manager/flat-file-connection-manager.md)Flat, [Editor gestione connessione file flat &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md), [Editor gestione connessione file flat &#40;pagina colonne&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md), [Editor gestione connessione file flat &#40;pagina avanzate&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)  
  
 **Aggiorna tabelle**  
 Consente di aggiornare l'elenco di tabelle e di viste.  
  
## <a name="format-dynamic-options"></a>Opzioni dinamiche di Format  
  
### <a name="format--use-file"></a>Format = Usa file  
 **FormatFile**  
 Digitare il percorso del file di formato oppure fare clic sui puntini di sospensione **(...)** per trovare il file di formato.  
  
### <a name="format--specify"></a>Format = Specifica  
 `RowDelimiter`  
 Consente di specificare il delimitatore di riga nel file di origine. Il valore predefinito è **{CR} {LF}**.  
  
 `ColumnDelimiter`  
 Consente di specificare il delimitatore di colonna nel file di origine. Il valore predefinito è **Tabulazione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Inserimento bulk &#40;pagina generale&#41;](../../2014/integration-services/bulk-insert-task-editor-general-page.md)   
 [Editor attività Inserimento bulk &#40;pagina Opzioni&#41;](../../2014/integration-services/bulk-insert-task-editor-options-page.md)   
 [Pagina Espressioni](expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Flusso di controllo](control-flow/control-flow.md)  
  
  
