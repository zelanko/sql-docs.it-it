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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e325793a7b703c445be836f6f427645acda3370
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68138853"
---
# <a name="is-odbc-the-answer"></a>Quando usare ODBC
Prima di affrontare il problema di interoperabilità, prendere in considerazione i seguenti aspetti: L'applicazione utilizzino ODBC affatto? Ciò può sembrare una domanda strano per porre in una Guida a ODBC, ma è, infatti, una legittima. ODBC non è stata progettata per sostituire completamente l'API di database nativa, né è stato progettato per fornire l'accesso al database in qualsiasi circostanza. È stato progettato per fornire un'interfaccia comune per i database e può essere gratuito ai programmatori di dover apprendere e mantenere i collegamenti a più database.  
  
 Le applicazioni personalizzate sono i candidati ideali per le API di database nativo. Il motivo principale è che le applicazioni personalizzate spesso funziona con un DBMS singolo e non necessario per essere interoperabile. Database nativo API potrebbero ottenere una migliore rispetto a ODBC di esporre le funzionalità del sistema DBMS per un particolare e potrebbero esporre le funzionalità non esposte da ODBC. Inoltre, poiché gli sviluppatori di applicazioni personalizzate sono in genere familiari con l'API di database nativo per il sistema DBMS, c'è motivo little per informazioni su ODBC. Tuttavia, è interessante notare che per alcuni DBMS, ODBC è l'API di database nativo.  
  
 Quindi, quali applicazioni sono candidati per ODBC? I candidati migliori sono le applicazioni che funzionano con più di un sistema DBMS. Ciò include quasi tutte le applicazioni verticali e non generici. Contiene inoltre un numero di applicazioni personalizzate. Ad esempio, le applicazioni personalizzate che usano diversi DBMS diverse sono molto più semplice e più facili da scrivere con ODBC rispetto a più API native. E applicazioni personalizzate scritte con ODBC sono molto più semplice eseguire la migrazione di un'azienda si sposta da un DBMS a altro o distribuisce l'applicazione stessa con diversi DBMS.
