---
title: SQL statico | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81279903"
---
# <a name="static-sql"></a>SQL statico
L'oggetto SQL incorporato illustrato nell' [esempio SQL incorporato](../../odbc/reference/embedded-sql-example.md) è noto come SQL statico. Viene chiamato SQL statico perché le istruzioni SQL nel programma sono statiche. ovvero non cambiano ogni volta che viene eseguito il programma. Come descritto nella sezione precedente, queste istruzioni vengono compilate quando viene compilato il resto del programma.  
  
 SQL statico funziona correttamente in molte situazioni e può essere usato in qualsiasi applicazione per la quale l'accesso ai dati può essere determinato in fase di progettazione del programma. Un programma di immissione degli ordini, ad esempio, USA sempre la stessa istruzione per inserire un nuovo ordine e un sistema di prenotazione delle compagnie aeree Usa sempre la stessa istruzione per modificare lo stato di una postazione da disponibile a riservata. Ognuna di queste istruzioni verrebbe generalizzata tramite l'utilizzo di variabili host. è possibile inserire valori diversi in un ordine di vendita ed è possibile riservare sedi diverse. Poiché tali istruzioni possono essere hardcoded nel programma, tali programmi hanno il vantaggio che le istruzioni devono essere analizzate, convalidate e ottimizzate una sola volta in fase di compilazione. Questo comporta un codice relativamente rapido.
