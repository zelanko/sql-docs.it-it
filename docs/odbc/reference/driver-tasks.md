---
title: Attività del driver | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2e2ed50ac3f9e914953abdd64907199a5f978af2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915466"
---
# <a name="driver-tasks"></a>Attività dei driver
Le attività specifiche eseguite dai driver includono:  
  
-   Connessione e disconnessione dall'origine dati.  
  
-   Verifica degli errori di funzione non controllati da Gestione driver.  
  
-   Avvio delle transazioni; Questa operazione è trasparente per l'applicazione.  
  
-   Invio di istruzioni SQL all'origine dati per l'esecuzione. Il driver deve modificare SQL ODBC in SQL specifico di DBMS; Questa operazione è spesso limitata alla sostituzione delle clausole Escape definite da ODBC con SQL specifico di DBMS.  
  
-   Invio e recupero di dati dall'origine dati, inclusa la conversione di tipi di dati in base a quanto specificato dall'applicazione.  
  
-   Mapping di errori specifici di DBMS a sqlstates ODBC.
