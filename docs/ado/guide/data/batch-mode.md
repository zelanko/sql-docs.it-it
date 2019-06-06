---
title: Modalità batch | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], batch mode
- batch mode [ADO]
- updating data [ADO], batch mode
ms.assetid: 0cb548e0-fcb4-4c49-98c8-be287911f826
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 39130be0e6be31700f70002726f3aaf674aa4c82
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700924"
---
# <a name="batch-mode"></a>Modalità batch
Attiva la modalità batch quando il **LockType** è impostata su **adLockBatchOptimistic** e l'aggiornamento in batch è supportato dal provider. Alcune impostazioni del tipo di blocco non sono disponibili in base alla posizione del cursore. Ad esempio, un tipo di blocco pessimistico non è disponibile quando il **CursorLocation** è impostata su **adUseClient**. Al contrario, un provider non può supportare un blocco ottimistico batch quando il cursore si trova nel server. È consigliabile usare l'aggiornamento in blocco con un solo cursore statico o keyset.  
  
 Il **UpdateBatch** metodo viene usato per inviare **Recordset** modifiche memorizzate nel buffer di copia al server per aggiornare l'origine dati. Nella sezione seguente, verrà aperta una **Recordset** in modalità batch, apportare modifiche al buffer di copia e quindi inviare le modifiche all'origine dati tramite una chiamata a **UpdateBatch**.  
  
 Questa sezione contiene i seguenti argomenti:  
  
-   [Invio di aggiornamenti: Metodo UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtro per record aggiornati](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Gestione degli aggiornamenti non riusciti](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Rilevamento e risoluzione di conflitti](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Disconnessione e riconnessione del recordset](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Aggiornamento dei risultati join: Tabella univoca](../../../ado/guide/data/updating-joined-results-unique-table.md)
