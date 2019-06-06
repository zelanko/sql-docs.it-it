---
title: Riepilogo dei gestori eventi ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- events [ADO], about event handlers
- event handlers [ADO]
ms.assetid: b34f4472-5e04-4a2c-ab64-38d6eca31a69
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f1901892b3e48446f3598b24ebb0a529360b9edf
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702651"
---
# <a name="ado-connection-and-recordset-events"></a>Connessione ADO e gli eventi di Recordset
Due oggetti ADO possono generare eventi: i [Connection](../../../ado/reference/ado-api/connection-object-ado.md) oggetto e il [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto. Il **ConnectionEvent** famiglia relativa alle operazioni sulle **connessione** oggetto e il **RecordsetEvent** famiglia relativa alle operazioni sul  **Recordset** oggetto.

-   **Eventi connessione**: Gli eventi vengono emessi quando una transazione su una connessione viene avviata, viene eseguito il commit o rollback; Quando un [comandi](../../../ado/reference/ado-api/command-object-ado.md) viene eseguita; quando viene generato un avviso durante una **evento di connessione** operazione; o quando un **connessione** inizia o finisce.

-   **Gli eventi di recordset**: Gli eventi vengono emessi intorno a operazioni di recupero asincrono, nonché quando si esplorano le righe di una **Recordset** dell'oggetto, modificare un campo in una riga di una **Recordset**, modificata una riga in un  **Recordset**, aprire una **Recordset** con un cursore lato server, chiudere un **Recordset**, o apportare qualsiasi modifica nel **Recordset**.

 Le tabelle seguenti riepilogano gli eventi e le relative descrizioni.

|ConnectionEvent|Descrizione|
|---------------------|-----------------|
|[BeginTransComplete, CommitTransComplete, RollbackTransComplete](../../../ado/reference/ado-api/begintranscomplete-committranscomplete-and-rollbacktranscomplete-events-ado.md)|**Gestione delle transazioni** -notifica che la transazione corrente sulla connessione è stata avviata, il commit o rollback.|
|[WillConnect](../../../ado/reference/ado-api/willconnect-event-ado.md), [ConnectComplete, Disconnect](../../../ado/reference/ado-api/connectcomplete-and-disconnect-events-ado.md)|**Gestione delle connessioni** -notifica che è possibile avviare la connessione corrente, è stata avviata o è scaduta.|
|[WillExecute](../../../ado/reference/ado-api/willexecute-event-ado.md), [ExecuteComplete](../../../ado/reference/ado-api/executecomplete-event-ado.md)|**Comando di gestione delle esecuzioni** -notifica che l'esecuzione del comando corrente per la connessione verrà avviato o è scaduta.|
|[InfoMessage](../../../ado/reference/ado-api/infomessage-event-ado.md)|**Informativo** -notifica dell'esistenza di informazioni aggiuntive sull'operazione corrente.|

|RecordsetEvent|Descrizione|
|--------------------|-----------------|
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md), [FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|**Stato di recupero** -notifica dello stato di avanzamento di un'operazione di recupero di dati o che l'operazione di recupero è stata completata. Questi eventi sono disponibili solo se il **Recordset** è stato aperto tramite un cursore lato client.|
|[WillChangeField, FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|**Gestione delle modifiche campo** -notifica che verrà modificato il valore del campo corrente o è stato modificato.|
|[WillMove, MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), [EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|**Gestione dello spostamento** -notifica che la riga corrente di posizionare in un **Recordset** cambia, è stato modificato o ha raggiunto la fine del **Recordset**.|
|[WillChangeRecord, RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|**Gestione delle modifiche di riga** -notifica che qualcosa nella riga corrente del **Recordset** cambierà o è stato modificato.|
|[WillChangeRecordset, RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|**Gestione dei cambiamenti di recordset** -notifica che qualcosa nell'attuale **Recordset** cambierà o è stato modificato.|

## <a name="see-also"></a>Vedere anche
 [Creazione di istanze evento ADO dal linguaggio](../../../ado/guide/data/ado-event-instantiation-by-language.md) [eventi ADO](../../../ado/reference/ado-api/ado-events.md) [parametri evento](../../../ado/guide/data/event-parameters.md) [sull'interagiscono tra i gestori eventi](../../../ado/guide/data/how-event-handlers-work-together.md) [tipi di eventi](../../../ado/guide/data/types-of-events.md)
