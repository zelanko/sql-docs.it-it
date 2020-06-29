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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: b2cd722fd8520ff011c0d57040a55d624178e15e
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85439168"
---
# <a name="bulk-insert-task-editor-connection-page"></a>Editor attività Inserimento bulk (pagina Connessione)
  Usare la pagina **Connessione** della finestra di dialogo **Editor attività Inserimento bulk** per specificare l'origine e la destinazione dell'operazione di inserimento bulk e il formato da usare.  
  
 Per altre informazioni sulle operazioni di inserimento bulk, vedere [Attività Inserimento bulk](control-flow/bulk-insert-task.md) e [File di formato per l'importazione o l'esportazione di dati &#40;SQL Server&#41;](../relational-databases/import-export/format-files-for-importing-or-exporting-data-sql-server.md).  
  
## <a name="options"></a>Opzioni  
 **Connection**  
 Selezionare una gestione connessione OLE DB nell'elenco oppure fare clic su \<**New connection...**> per creare una nuova connessione.  
  
 **Argomenti correlati:** [Gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md), [Configura gestione connessione OLE DB](../../2014/integration-services/configure-ole-db-connection-manager.md)  
  
 **DestinationTable**  
 Consente di digitare il nome della tabella o della vista di destinazione o di selezionare una tabella o una vista nell'elenco.  
  
 **Formato**  
 Consente di selezionare l'origine del formato per l'inserimento bulk. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Usa file**|Consente di selezionare un file contenente la specifica di formato. Selezionando questa opzione viene visualizzata l'opzione dinamica **FormatFile**.|  
|**Specifica**|Consente di specificare il formato. Selezionando questa opzione vengono visualizzate le opzioni dinamiche `RowDelimiter` e `ColumnDelimiter` .|  
  
 **File**  
 Selezionare una gestione connessione file o file flat nell'elenco oppure fare clic su \<**New connection...**> per creare una nuova connessione.  
  
 Il percorso del file è relativo al Motore di database di SQL Server specificato nella gestione connessione per questa attività. Il file di testo deve essere accessibile dal Motore di database di SQL Server in un disco rigido locale sul server oppure tramite un'unità condivisa o di cui è stato eseguito il mapping a SQL Server. Non è possibile accedere al file tramite SSIS Runtime.  
  
 Se si accede al file di origine utilizzando una gestione connessione file flat, l'attività Inserimento bulk non utilizzerà il formato specificato nella gestione connessione file flat, ma userà il formato specificato in un file di formato o i valori delle proprietà RowDelimiter e ColumnDelimiter dell'attività.  
  
 **Argomenti correlati:** [Gestione connessione file](connection-manager/file-connection-manager.md), [Editor gestione connessione file](../../2014/integration-services/file-connection-manager-editor.md), [Gestione connessione file flat](connection-manager/flat-file-connection-manager.md), [Editor gestione connessione file flat &#40;pagina generale&#41;](general-page-of-integration-services-designers-options.md), [Editor gestione connessione file flat &#40;pagina Colonne&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md), [Editor gestione connessione file flat &#40;pagina Avanzate&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)  
  
 **Aggiorna tabelle**  
 Consente di aggiornare l'elenco di tabelle e di viste.  
  
## <a name="format-dynamic-options"></a>Opzioni dinamiche di Format  
  
### <a name="format--use-file"></a>Format = Usa file  
 **FormatFile**  
 Digitare il percorso del file di formato oppure fare clic sul pulsante con i puntini di sospensione **(...)** per individuare il file di formato.  
  
### <a name="format--specify"></a>Format = Specifica  
 `RowDelimiter`  
 Consente di specificare il delimitatore di riga nel file di origine. Il valore predefinito è **{CR} {LF}**.  
  
 `ColumnDelimiter`  
 Consente di specificare il delimitatore di colonna nel file di origine. Il valore predefinito è **Tabulazione**.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor attività Inserimento bulk &#40;pagina generale&#41;](../../2014/integration-services/bulk-insert-task-editor-general-page.md)   
 [Editor attività Inserimento bulk &#40;pagina Opzioni&#41;](../../2014/integration-services/bulk-insert-task-editor-options-page.md)   
 [Pagina espressioni](expressions/expressions-page.md)   
 [BULK INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/bulk-insert-transact-sql)   
 [Flusso di controllo](control-flow/control-flow.md)  
  
  
