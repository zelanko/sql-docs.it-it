---
title: Proprietà Interoperabilità . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC]
- interoperability [ODBC], about interoperability
ms.assetid: 43b7c849-9d59-4002-9977-9e2c8730b859
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 31b20a696c601ff91c591e4c717f468beca34e36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306222"
---
# <a name="interoperability"></a>Interoperabilità
*L'interoperabilità* è la capacità di una singola applicazione di operare con molti DBS diversi. La necessità di scrivere applicazioni generiche interoperabili è stato uno dei principali fattori che hanno portato allo sviluppo di ODBC. Tuttavia, l'interoperabilità non è un percorso semplice seguito da "non interoperabile" a "completamente interoperabile". Il percorso ha molti rami e ognuno richiede compromessi tra funzionalità, velocità, complessità del codice e tempo di sviluppo.  
  
 Il processo di scrittura di un'applicazione interoperabile segue diversi passaggi:  
  
1.  Decidere se l'applicazione utilizzerà ODBC.  
  
2.  Scegliere un livello di interoperabilità e decidere quali compromessi sono necessari per raggiungere tale livello.  
  
3.  Scrivere codice interoperabile e testarlo nel modo più completo possibile.  
  
 Va notato che l'interoperabilità è principalmente il dominio del writer dell'applicazione. I driver sono progettati per funzionare con un singolo DBMS e, per definizione, non sono interoperabili. Essi svolgono un ruolo nell'interoperabilità implementando correttamente ed esponendo ODBC su un singolo DBMS.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Quando usare ODBC](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Scelta di un livello di interoperabilità](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinazione dei DBMS e dei driver di destinazione](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Considerazione delle funzionalità di database da usare](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Lunghezza del ciclo del prodotto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Scrittura di un'applicazione interoperativa](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Test delle applicazioni interoperative](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
