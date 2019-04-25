---
title: Interoperabilità delle istruzioni SQL | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c4ead7cf96ada6d6055bc676ecf4610f2cf4c8f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62446661"
---
# <a name="interoperability-of-sql-statements"></a>Interoperabilità delle istruzioni SQL
Come il resto di un'applicazione, le istruzioni SQL possono essere interoperabili o specifici del DBMS. E come gli altri componenti dell'applicazione, deve essere la scelta della modalità interoperative istruzioni SQL varia a seconda del tipo di applicazione. Le applicazioni personalizzate sono meno probabile che utilizzare istruzioni SQL interoperative perché sono in genere progettate per sfruttare le funzionalità di uno o probabilmente due DBMS. Applicazioni generiche utilizzano istruzioni SQL interoperative perché sono progettate per funzionare con un'ampia gamma di DBMS. E applicazioni verticali in genere rientrano in un punto intermedio, richiedono un certo livello di funzionalità, ma in caso contrario, tramite istruzioni SQL interoperative.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Scelta di una grammatica SQL](../../../odbc/reference/develop-app/choosing-an-sql-grammar.md)  
  
-   [Creazione di istruzioni SQL interoperative](../../../odbc/reference/develop-app/constructing-interoperable-sql-statements.md)
