---
description: Quando usare ODBC
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
ms.openlocfilehash: 7a51c4248a041d65f00ec1846f60788cded68f7b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476603"
---
# <a name="is-odbc-the-answer"></a>Quando usare ODBC
Prima di approfondire la domanda di interoperabilità, prendere in considerazione la domanda seguente: se l'applicazione usa ODBC? Questo potrebbe sembrare una domanda strana da porre in una guida a ODBC, ma è in realtà uno dei più legittimi. ODBC non è stato progettato per sostituire completamente le API del database nativo, né per fornire l'accesso al database in tutte le circostanze. È stato progettato per fornire un'interfaccia comune ai database ed è stato progettato per liberare i programmatori di applicazioni che non devono più conoscere e gestire i collegamenti a più database.  
  
 Le applicazioni personalizzate sono candidati principali per le API di database native. Il motivo principale è che le applicazioni personalizzate spesso funzionano con un singolo sistema DBMS e non devono essere interoperative. Le API di database native possono offrire un lavoro migliore rispetto a ODBC per esporre le funzionalità di un sistema DBMS specifico e possono esporre funzionalità non esposte da ODBC. Inoltre, poiché gli sviluppatori di applicazioni personalizzate hanno in genere familiarità con l'API del database nativo per il sistema DBMS, non esiste un motivo per conoscere ODBC. Tuttavia, è interessante notare che, per alcuni DBMS, ODBC è l'API del database nativo.  
  
 Quali applicazioni sono candidati per ODBC? I candidati migliori sono applicazioni che funzionano con più di un DBMS. Sono incluse praticamente tutte le applicazioni generiche e verticali. Include inoltre una serie di applicazioni personalizzate. Ad esempio, le applicazioni personalizzate che usano più DBMS diversi sono molto più semplici e più pulite per la scrittura con ODBC rispetto a più API native. E le applicazioni personalizzate scritte con ODBC sono molto più semplici da migrare quando un'azienda si sposta da un sistema DBMS a un altro o distribuisce la stessa applicazione su DBMS diversi.
