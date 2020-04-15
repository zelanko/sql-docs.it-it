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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8afba3b3b8c8fee1307473c790186d509b37d982
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294851"
---
# <a name="concurrency-control"></a>Controllo della concorrenza
*La concorrenza* è la capacità di due transazioni di utilizzare gli stessi dati contemporaneamente e con l'aumento dell'isolamento delle transazioni viene in genere ridotto. Ciò è dovuto al fatto che l'isolamento delle transazioni viene in genere implementato bloccando le righe e, poiché vengono bloccate più righe, è possibile completare un numero inferiore di transazioni senza essere bloccate almeno temporaneamente da una riga bloccata. Sebbene la concorrenza ridotta sia generalmente accettata come compromesso per i livelli di isolamento delle transazioni più elevati necessari per mantenere l'integrità del database, può diventare un problema nelle applicazioni interattive con un'elevata attività di lettura/scrittura che utilizzano cursori.  
  
 Si supponga, ad esempio, che un'applicazione esegua l'istruzione SQL **SELECT \* FROM Orders**. Chiama **SQLFetchScroll** per scorrere il set di risultati e consente all'utente di aggiornare, eliminare o inserire gli ordini. Dopo che l'utente aggiorna, elimina o inserisce un ordine, l'applicazione esegue il commit della transazione.  
  
 Se il livello di isolamento è Lettura ripetibile, la transazione, a seconda di come viene implementata, potrebbe bloccare ogni riga restituita da **SQLFetchScroll**. Se il livello di isolamento è Serializable, la transazione potrebbe bloccare l'intera tabella Orders. In entrambi i casi, la transazione rilascia i blocchi solo quando viene eseguito il commit o il rollback. Quindi, se l'utente impiega molto tempo a leggere gli ordini e poco tempo ad aggiornarli, eliminarli o inserirli, la transazione potrebbe facilmente bloccare un gran numero di righe, rendendole non disponibili ad altri utenti.  
  
 Si tratta di un problema anche se il cursore è di sola lettura e l'applicazione consente all'utente di leggere solo gli ordini esistenti. In questo caso, l'applicazione esegue il commit della transazione e rilascia blocchi quando chiama **SQLCloseCursor** (in modalità di commit automatico) o **SQLEndTran** (in modalità di commit manuale).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di concorrenza](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md)
