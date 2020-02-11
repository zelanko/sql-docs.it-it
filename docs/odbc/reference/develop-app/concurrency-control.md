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
ms.openlocfilehash: 7c541bf28c1d4c7ec2e2041201bd7c168625bb34
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68083259"
---
# <a name="concurrency-control"></a>Controllo della concorrenza
La *concorrenza* è la capacità di due transazioni di utilizzare contemporaneamente gli stessi dati e con un maggiore isolamento delle transazioni viene in genere ridotta la concorrenza. Questo è dovuto al fatto che l'isolamento delle transazioni viene in genere implementato tramite il blocco delle righe e, man mano che vengono bloccate più righe, è possibile completare un minor numero di transazioni senza bloccarle almeno temporaneamente da una riga bloccata. Mentre la concorrenza ridotta viene generalmente accettata come compromesso per i livelli di isolamento delle transazioni più elevati necessari per mantenere l'integrità del database, può diventare un problema nelle applicazioni interattive con un'attività di lettura/scrittura elevata che utilizza i cursori.  
  
 Si supponga, ad esempio, che un'applicazione esegua l'istruzione SQL **Select \* from Orders**. Chiama **SQLFetchScroll** per scorrere il set di risultati e consente all'utente di aggiornare, eliminare o inserire ordini. Dopo l'aggiornamento, l'eliminazione o l'inserimento di un ordine da parte dell'utente, l'applicazione eseguirà il commit della transazione.  
  
 Se il livello di isolamento è Repeatable Read, la transazione potrebbe variare a seconda della modalità di implementazione, ovvero bloccare ogni riga restituita da **SQLFetchScroll**. Se il livello di isolamento è serializzabile, è possibile che la transazione blocchi l'intera tabella Orders. In entrambi i casi, la transazione rilascia i blocchi solo quando ne viene eseguito il commit o il rollback. Quindi, se l'utente dedica molto tempo alla lettura degli ordini e non aggiorna, Elimina o inserisce, la transazione potrebbe bloccare facilmente un numero elevato di righe, rendendole non disponibili ad altri utenti.  
  
 Si tratta di un problema anche se il cursore è di sola lettura e l'applicazione consente all'utente di leggere solo gli ordini esistenti. In questo caso, l'applicazione esegue il commit della transazione e rilascia i blocchi quando chiama **SQLCloseCursor** (in modalità autocommit) o **SQLEndTran** (in modalità di commit manuale).  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Tipi di concorrenza](../../../odbc/reference/develop-app/concurrency-types.md)  
  
-   [Concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md)
