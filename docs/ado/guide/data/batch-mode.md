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
author: rothja
ms.author: jroth
ms.openlocfilehash: b7e4ce2e8928ac7b4225ae58b25c6610c64832f7
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761247"
---
# <a name="batch-mode"></a>Modalità batch
La modalità batch è attiva quando la proprietà **LockType** è impostata su **adLockBatchOptimistic** e l'aggiornamento in batch è supportato dal provider. Determinate impostazioni del tipo di blocco non sono disponibili a seconda della posizione del cursore. Un tipo di blocco pessimistico, ad esempio, non è disponibile quando **CursorLocation** è impostato su **adUseClient**. Viceversa, un provider non è in grado di supportare un blocco ottimistico batch quando la posizione del cursore si trova nel server. È consigliabile utilizzare l'aggiornamento batch solo con un keyset o un cursore statico.  
  
 Il metodo **UpdateBatch** viene utilizzato per inviare le modifiche del **Recordset** mantenute nel buffer di copia al server per aggiornare l'origine dati. Nella sezione seguente verrà aperto un **Recordset** in modalità batch, vengono apportate modifiche al buffer di copia e quindi le modifiche vengono inviate all'origine dati mediante una chiamata a **UpdateBatch**.  
  
 Questa sezione contiene i seguenti argomenti:  
  
-   [Invio di aggiornamenti: metodo UpdateBatch](../../../ado/guide/data/sending-the-updates-updatebatch-method.md)  
  
-   [Filtro per i record aggiornati](../../../ado/guide/data/filtering-for-updated-records.md)  
  
-   [Gestione degli aggiornamenti non riusciti](../../../ado/guide/data/dealing-with-failed-updates.md)  
  
-   [Rilevamento e risoluzione di conflitti](../../../ado/guide/data/detecting-and-resolving-conflicts.md)  
  
-   [Disconnessione e riconnessione del recordset](../../../ado/guide/data/disconnecting-and-reconnecting-the-recordset.md)  
  
-   [Aggiornamento dei risultati uniti in join: tabella univoca](../../../ado/guide/data/updating-joined-results-unique-table.md)
