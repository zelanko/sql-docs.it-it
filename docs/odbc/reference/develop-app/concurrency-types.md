---
title: Tipi di concorrenza | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 63d7c7dce51fe4f514232cfd0d5ae2e5abeb5b70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083179"
---
# <a name="concurrency-types"></a>Tipi di concorrenza
Per risolvere il problema di riduzione della concorrenza nei cursori, ODBC espone quattro diversi tipi di concorrenza dei cursori:  
  
-   **Sola lettura** il cursore può leggere i dati, ma non è possibile aggiornare o eliminare dati. Questo è il tipo di concorrenza predefinita. Anche se il sistema DBMS potrebbe bloccare le righe per imporre la lettura ripetibile e livelli di isolamento serializzabile, può usare i blocchi in lettura invece di blocchi in scrittura. Ciò comporta una concorrenza più elevata perché almeno possono leggere i dati.  
  
-   **Blocco** il cursore utilizza il livello più basso di blocco necessario per assicurarsi che può aggiornare o eliminare righe nel set di risultati. Ciò comporta in genere i livelli di concorrenza molto bassa, soprattutto ai livelli di isolamento delle transazioni Repeatable Read e Serializable.  
  
-   **La concorrenza ottimistica con le versioni di riga e la concorrenza ottimistica con valori** il cursore utilizza la concorrenza ottimistica: Aggiorna o Elimina le righe solo se non sono cambiati dall'ultima lettura. Per rilevare le modifiche, confronta le versioni delle righe o valori. Non c'è garanzia che il cursore sarà in grado di aggiornare o eliminare una riga, ma la concorrenza è molto maggiore rispetto a quando il blocco viene utilizzato. Per altre informazioni, vedere la sezione seguente [la concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 Un'applicazione specifica quale tipo di concorrenza vuole che il cursore da utilizzare con l'attributo di istruzione SQL_ATTR_CONCURRENCY. Per determinare quali tipi sono supportati, chiama **SQLGetInfo** con l'opzione SQL_SCROLL_CONCURRENCY.
