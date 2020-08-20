---
description: Interoperabilità
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a404ee6de56cbd8b5605eca640fdf0e065f16d79
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476613"
---
# <a name="interoperability"></a>Interoperabilità
L' *interoperabilità* è la capacità di una singola applicazione di operare con molti sistemi DBMS diversi. La necessità di scrivere applicazioni generiche interoperative era uno dei fattori principali che derivano dallo sviluppo di ODBC. Tuttavia, l'interoperabilità non è un percorso semplice seguito da "non interoperativo" a "completamente interoperativo". Il percorso ha molti rami, ognuno dei quali richiede compromessi tra funzionalità, velocità, complessità del codice e tempi di sviluppo.  
  
 Il processo di scrittura di un'applicazione interoperativa segue diversi passaggi:  
  
1.  Decidere se l'applicazione userà ODBC.  
  
2.  Scegliere un livello di interoperabilità e decidere quali compromessi sono necessari per raggiungere tale livello.  
  
3.  Scrivere codice interoperativo e testarlo nel modo più completo possibile.  
  
 Si noti che l'interoperabilità è principalmente il dominio del writer di applicazioni. I driver sono progettati per funzionare con un singolo sistema DBMS e, per definizione, non sono interoperativi. Svolgono un ruolo nell'interoperabilità implementando ed esponendo correttamente ODBC in un singolo sistema DBMS.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Quando usare ODBC](../../../odbc/reference/develop-app/is-odbc-the-answer.md)  
  
-   [Scelta di un livello di interoperabilità](../../../odbc/reference/develop-app/choosing-a-level-of-interoperability.md)  
  
-   [Determinazione dei DBMS e dei driver di destinazione](../../../odbc/reference/develop-app/determining-the-target-dbmss-and-drivers.md)  
  
-   [Considerazione delle funzionalità di database da usare](../../../odbc/reference/develop-app/considering-database-features-to-use.md)  
  
-   [Lunghezza del ciclo del prodotto](../../../odbc/reference/develop-app/length-of-the-product-cycle.md)  
  
-   [Scrittura di un'applicazione interoperativa](../../../odbc/reference/develop-app/writing-an-interoperable-application.md)  
  
-   [Test delle applicazioni interoperative](../../../odbc/reference/develop-app/testing-interoperable-applications.md)
