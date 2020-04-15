---
title: Attività del driver Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC architecture [ODBC], drivers
- drivers [ODBC], tasks
ms.assetid: 184c795a-c2e8-4d20-9902-12e60b2f0e45
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1b30df63a3c955d2ed074ab13649ea55c21a6da7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294201"
---
# <a name="driver-tasks"></a>Attività dei driver
Le attività specifiche eseguite dai conducenti includono:  
  
-   Connessione e disconnessione dall'origine dati.  
  
-   Controllo degli errori di funzione non controllato da Gestione Driver.  
  
-   Inizio delle transazioni; questo è trasparente per l'applicazione.  
  
-   Invio di istruzioni SQL all'origine dati per l'esecuzione. Il driver deve modificare ODBC SQL in SQL specifico del DBMS. questo è spesso limitato alla sostituzione di clausole di escape definite da ODBC con SQL specifico DBMS.  
  
-   Invio e recupero di dati dall'origine dati, inclusa la conversione dei tipi di dati come specificato dall'applicazione.  
  
-   Mapping degli errori specifici del DBMS a SQLSTATE ODBC.
