---
title: Quando usare ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], ODBC
ms.assetid: bfa5e6ee-5979-42a9-be6f-a84d1ee7a54c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f3716acbcc1b8ea648b5edc03e277983936da557
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288092"
---
# <a name="is-odbc-the-answer"></a>Quando usare ODBC
Prima di approfondire la questione dell'interoperabilità, considerare la seguente domanda: l'applicazione deve utilizzare ODBC? Questa potrebbe sembrare una domanda strana da porre in una guida a ODBC, ma è, in realtà, una domanda legittima. ODBC non è stato progettato per sostituire completamente le API di database native, né è stato progettato per fornire l'accesso al database in tutte le circostanze. È stato progettato per fornire un'interfaccia comune ai database ed è stato progettato per liberare i programmatori di applicazioni di dover conoscere e mantenere i collegamenti a più database.  
  
 Le applicazioni personalizzate sono candidati principali per le API di database native. Il motivo principale è che le applicazioni personalizzate spesso funzionano con un singolo DBMS e non hanno bisogno di essere interoperabili. Le API di database native potrebbero eseguire un lavoro migliore rispetto a ODBC nell'esporre le funzionalità di un dbMS specifico e potrebbero esporre funzionalità non esposte da ODBC. Inoltre, poiché gli sviluppatori di applicazioni personalizzate hanno in genere familiarità con l'API di database nativa per il DBMS, non c'è motivo di imparare ODBC. Tuttavia, è interessante notare che per alcuni DBS, ODBC è l'API del database nativo.  
  
 Quindi, quali applicazioni sono candidati per ODBC? I candidati migliori sono applicazioni che funzionano con più di un DBMS. Questo include praticamente tutte le applicazioni generiche e verticali. Include anche una serie di applicazioni personalizzate. Ad esempio, le applicazioni personalizzate che utilizzano diversi DBSCR diversi sono molto più semplici e più semplici da scrivere con ODBC rispetto a più API native. E le applicazioni personalizzate scritte con ODBC sono molto più facili da migrare quando una società passa da un DBMS a un altro o distribuisce la stessa applicazione in DBMS diversi.
