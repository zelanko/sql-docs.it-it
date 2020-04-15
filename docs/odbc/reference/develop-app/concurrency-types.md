---
title: Tipi di concorrenza - Documenti Microsoft
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
- locking concurrency control [ODBC]
- optimistic concurrency [ODBC]
- read-only concurrency control [ODBC]
ms.assetid: 46762ae5-17dd-4777-968e-58156f470fe1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 642301d09c5aa189276db534e58aca0c5e00e3ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299101"
---
# <a name="concurrency-types"></a>Tipi di concorrenza
Per risolvere il problema della concorrenza ridotta nei cursori, ODBC espone quattro diversi tipi di concorrenza del cursore:  
  
-   **Sola lettura** Il cursore può leggere i dati ma non aggiornare o eliminare i dati. Questo è il tipo di concorrenza predefinito. Anche se il DBMS potrebbe bloccare le righe per applicare i livelli di isolamento Ripetibile lettura e Serializable, è possibile utilizzare blocchi di lettura anziché blocchi di scrittura. Ciò comporta una maggiore concorrenza perché altre transazioni possono almeno leggere i dati.  
  
-   **Blocco** Il cursore utilizza il livello più basso di blocco necessario per assicurarsi che sia possibile aggiornare o eliminare le righe nel set di risultati. Ciò comporta in genere livelli di concorrenza molto bassi, in particolare ai livelli di isolamento delle transazioni ripetibili di lettura e serializzazione.  
  
-   **Concorrenza ottimistica tramite versioni di riga e concorrenza ottimistica tramite valoriOptimistic concurrency using row versions and optimistic concurrency using values** Il cursore utilizza la concorrenza ottimistica: aggiorna o elimina le righe solo se non sono state modificate dopo l'ultima lettura. Per rilevare le modifiche, confronta le versioni o i valori delle righe. Non esiste alcuna garanzia che il cursore sarà in grado di aggiornare o eliminare una riga, ma la concorrenza è molto più alta rispetto a quando viene utilizzato il blocco. Per ulteriori informazioni, vedere la sezione seguente, [Concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Un'applicazione specifica il tipo di concorrenza che si desidera che il cursore da utilizzare con l'attributo di istruzione SQL_ATTR_CONCURRENCY. Per determinare i tipi supportati, chiama **SQLGetInfo** con l'opzione SQL_SCROLL_CONCURRENCY.
