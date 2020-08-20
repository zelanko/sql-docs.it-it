---
description: Tipi di concorrenza
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d55740b71d4e9a7d3b8d22400da0c5b3d94e73d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461543"
---
# <a name="concurrency-types"></a>Tipi di concorrenza
Per risolvere il problema relativo alla riduzione della concorrenza nei cursori, ODBC espone quattro tipi diversi di concorrenza del cursore:  
  
-   Sola **lettura** Il cursore può leggere i dati ma non può aggiornare o eliminare i dati. Si tratta del tipo di concorrenza predefinito. Sebbene il sistema DBMS possa bloccare le righe per applicare i livelli di isolamento Repeatable Read e Serializable, può utilizzare i blocchi Read anziché i blocchi Write. Ciò comporta una concorrenza più elevata perché altre transazioni possono almeno leggere i dati.  
  
-   **Blocco** di Il cursore utilizza il livello di blocco più basso necessario per verificare che sia in grado di aggiornare o eliminare righe nel set di risultati. Questo in genere comporta livelli di concorrenza molto bassi, soprattutto a livello di isolamento delle transazioni Repeatable Read e Serializable.  
  
-   **Concorrenza ottimistica che utilizza versioni di riga e concorrenza ottimistica utilizzando valori** Il cursore usa la concorrenza ottimistica: Aggiorna o Elimina le righe solo se non sono state modificate dall'ultima lettura. Per rilevare le modifiche, vengono confrontate le versioni di riga o i valori. Non vi è alcuna garanzia che il cursore sia in grado di aggiornare o eliminare una riga, ma la concorrenza è molto più elevata rispetto a quando si usa il blocco. Per ulteriori informazioni, vedere la sezione seguente, [concorrenza ottimistica](../../../odbc/reference/develop-app/optimistic-concurrency.md).  
  
 In un'applicazione viene specificato il tipo di concorrenza che si desidera venga utilizzato dal cursore con l'attributo dell'istruzione SQL_ATTR_CONCURRENCY. Per determinare quali tipi sono supportati, viene chiamato **SQLGetInfo** con l'opzione SQL_SCROLL_CONCURRENCY.
