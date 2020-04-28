---
title: Interoperabilità di istruzioni SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC]
- interoperability of SQL statements [ODBC], about interoperability
ms.assetid: 3b24c499-829c-4e65-90cf-a3a0f6d0a186
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3d7a76c67096d2e76fe1cd3d4b15f73122699e7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302802"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilità delle istruzioni SQL
Come il resto di un'applicazione, le istruzioni SQL possono essere interoperative o specifiche del sistema DBMS. E come il resto dell'applicazione, la scelta del modo in cui le istruzioni SQL interoperative devono dipendere dal tipo di applicazione. È meno probabile che le applicazioni personalizzate usino istruzioni SQL interoperative, in genere progettate per sfruttare le funzionalità di uno o forse due DBMS. Le applicazioni generiche utilizzano istruzioni SQL interoperative perché sono progettate per funzionare con un'ampia gamma di sistemi DBMS. E le applicazioni verticali in genere ricadeno tra di loro, richiedendo un certo livello di funzionalità, ma in caso contrario utilizzano istruzioni SQL interoperative.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Scelta di una grammatica SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Creazione di istruzioni SQL interoperative](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
