---
title: Interoperabilità | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8d5e4fbee458bec88461d3e2945a466c848d3345
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446488"
---
# <a name="interoperability"></a>Interoperabilità
*Interoperabilità* è la capacità di una singola applicazione di operare con maggior parte dei DBMS diversi. La necessità di scrivere applicazioni interoperative generiche è stato uno dei fattori principali iniziali allo sviluppo di ODBC. Tuttavia, l'interoperabilità non è un semplice percorso seguito da "non interoperabile" a "tutto intercambiabili." Il percorso contiene molti rami e ciascuna richiede compromessi tra funzionalità, velocità, la complessità del codice e in fase di sviluppo.  
  
 Il processo di scrittura di un'applicazione interoperativa segue passaggi diversi:  
  
1.  Decidere se l'applicazione utilizzerà ODBC.  
  
2.  Scelta di un livello di interoperabilità e decidere quali vantaggi e svantaggi sono necessari per raggiungere quel livello.  
  
3.  La scrittura di codice interoperabili e testarla per quanto possibile complete.  
  
 Tenere presente che l'interoperabilità è principalmente il dominio del writer dell'applicazione. I driver sono progettati per funzionare con un singolo DBMS e, per definizione, non sono interoperativi. Giocano un ruolo nell'interoperabilità correttamente implementando ed esposizione di ODBC in un singolo DBMS.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [La risposta è ODBC?](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Scelta di un livello di interoperabilità](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinazione dei DBMS e dei driver di destinazione](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Considerazione delle funzionalità di database da usare](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Lunghezza del ciclo del prodotto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Scrittura di un'applicazione interoperativa](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Test delle applicazioni interoperative](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
