---
title: Controllo della concorrenza | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], concurrency control
- concurrency control [ODBC]
ms.assetid: 75e4adb3-3d43-49c5-8c5e-8df96310d912
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2e54298e9c25777f10b92f322f1b1e6a3d94c243
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63191757"
---
# <a name="concurrency-control"></a>Controllo della concorrenza
*Concorrenza* è la possibilità di due transazioni utilizzano gli stessi dati allo stesso tempo, e delle transazioni isolamento in genere comporta una riduzione della concorrenza. Infatti di isolamento delle transazioni viene in genere implementato dal blocco di righe e come vengono bloccate altre righe, numero di transazioni può essere completato senza almeno temporaneamente bloccate da una riga bloccata. Mentre una riduzione della concorrenza in genere viene accettata come un compromesso per i livelli di isolamento delle transazioni superiore necessari mantenere l'integrità del database, può diventare un problema di applicazioni interattive con attività di lettura/scrittura elevata che utilizzano i cursori.  
  
 Ad esempio, si supponga che un'applicazione esegue l'istruzione SQL **selezionate \* FROM Orders**. Viene chiamato **SQLFetchScroll** per scorrere il risultato impostato e consente all'utente da aggiornare, eliminare o inserire gli ordini. Dopo che l'utente aggiorna, Elimina o inserisce un ordine, l'applicazione esegue il commit della transazione.  
  
 Se il livello di isolamento Repeatable Read, la transazione potrebbe - a seconda di come implementarlo - bloccare ogni riga restituita da **SQLFetchScroll**. Se il livello di isolamento è Serializable, la transazione potrà bloccare l'intera tabella Orders. In entrambi i casi, la transazione rilascia i blocchi solo quando è stato eseguito il commit o rollback. Pertanto, se l'utente impiega molto tempo per la lettura degli ordini e un tempo molto breve l'aggiornamento, eliminazione o la transazione è stato possibile inserire le informazioni, facilmente bloccare un numero elevato di righe, rendendoli disponibili ad altri utenti.  
  
 Si tratta di un problema, anche se il cursore è di sola lettura e l'applicazione consente all'utente di leggere solo gli ordini esistenti. In questo caso, l'applicazione esegue il commit della transazione e rilascia i blocchi, quando si chiama **SQLCloseCursor** (in modalità di commit automatico) o **SQLEndTran** (in modalità di commit manuale).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di concorrenza](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md)
