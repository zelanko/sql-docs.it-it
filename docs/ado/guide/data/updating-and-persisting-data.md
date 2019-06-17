---
title: L'aggiornamento e salvataggio di dati | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b251da97fe14abb8b10abe974c40b9adf0b37898
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699891"
---
# <a name="updating-and-persisting-data"></a>Aggiornamento e persistenza dei dati
Nei capitoli precedenti hanno illustrato come utilizzare ADO per recuperare i dati in un'origine dati, come spostarsi all'interno dei dati e anche come modificare i dati. Naturalmente, se l'obiettivo dell'applicazione è consentire agli utenti di apportare modifiche ai dati, è necessario conoscere le modalità salvare le modifiche. È ovvero possibile rendere persistenti la **Recordset** viene modificato in un file usando la **salvare** (metodo), oppure è possibile restituire le modifiche all'origine dati per l'uso di archiviazione il **Update** o  **Metodo UpdateBatch** metodi.  
  
 Nei capitoli precedenti, è stato modificato i dati in più righe del **Recordset**. ADO supporta due approcci di base in riguardanti l'aggiunta, eliminazione e la modifica di righe di dati.  
  
 La nozione prima è che le modifiche non vengono apportate immediatamente per il **Recordset**; in alternativa, sono state apportate a interna *buffer di copia*. Se si decide di non creare le modifiche, le modifiche nel buffer di copia vengono rimosse. Se si decide di mantenere le modifiche, le modifiche nel buffer di copia vengono applicate per il **Recordset**.  
  
 Nel secondo approccio è che le modifiche vengono propagate sia all'origine dati, non appena si dichiara il lavoro in una riga completa (vale a dire *immediata* modalità), o tutte le modifiche apportate a un set di righe vengono raccolti fino a quando non si dichiara il lavoro per il set completa (vale a dire *batch* modalità). Il **LockType** proprietà determina quando vengono apportate le modifiche all'origine dati sottostante. **adLockOptimistic** oppure **adLockPessimistic** specifica la modalità immediata, mentre **adLockBatchOptimistic** specifica la modalità batch. Il **CursorLocation** proprietà può influire sulla quale **LockType** impostazioni sono disponibili. Ad esempio, il **adLockPessimistic** impostazione non è supportata se il **CursorLocation** viene impostata su **adUseClient**.  
  
 In modalità immediata, ogni chiamata di **Update** metodo propaga le modifiche apportate all'origine dati. In modalità batch, ogni chiamata di **Update** o lo spostamento della posizione della riga corrente Salva le modifiche apportate al buffer di copia, ma solo le **UpdateBatch** metodo propaga le modifiche apportate all'origine dati.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Aggiornamento dei dati](../../../ado/guide/data/updating-data.md)  
  
-   [Persistenza dei dati](../../../ado/guide/data/persisting-data.md)
