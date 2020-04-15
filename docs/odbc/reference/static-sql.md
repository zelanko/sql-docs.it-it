---
title: Proprietà SQL statica . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- static SQL [ODBC]
- SQL [ODBC], embedded SQL
- SQL statements [ODBC], embedded SQL
- SQL statements [ODBC], static SQL
- embedded SQL [ODBC]
- SQL [ODBC], static SQL
ms.assetid: 667d92ec-fed9-4028-81d4-bb9ba867356a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55710d8ea734cba86ae5e4daa725f75e94e65a64
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81279903"
---
# <a name="static-sql"></a>SQL statico
Il codice SQL incorporato illustrato [nell'esempio Embedded SQL](../../odbc/reference/embedded-sql-example.md) è noto come SQL statico. Si chiama SQL statico perché le istruzioni SQL nel programma sono statiche; vale a dire, non cambiano ogni volta che il programma viene eseguito. Come descritto nella sezione precedente, queste istruzioni vengono compilate quando viene compilato il resto del programma.  
  
 SQL statico funziona bene in molte situazioni e può essere utilizzato in qualsiasi applicazione per cui l'accesso ai dati può essere determinato in fase di progettazione del programma. Ad esempio, un programma di inserimento degli ordini utilizza sempre la stessa istruzione per inserire un nuovo ordine e un sistema di prenotazione aerea utilizza sempre la stessa istruzione per modificare lo stato di un posto da disponibile a riservato. Ognuna di queste istruzioni sarebbe generalizzata attraverso l'uso di variabili host; In un ordine cliente possono essere inseriti valori diversi e possono essere prenotate postazioni diverse. Poiché tali istruzioni possono essere hardcoded nel programma, tali programmi hanno il vantaggio che le istruzioni devono essere analizzate, convalidate e ottimizzate solo una volta, in fase di compilazione. Questo si traduce in codice relativamente veloce.
