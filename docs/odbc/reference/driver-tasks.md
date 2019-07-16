---
title: Attività dei driver | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915466"
---
# <a name="driver-tasks"></a>Attività dei driver
Attività specifiche eseguite da tutti i driver includono:  
  
-   Alla connessione e disconnessione dall'origine dati.  
  
-   Il controllo degli errori di funzione non controllati da Gestione Driver.  
  
-   Avviare le transazioni. Ciò è trasparente per l'applicazione.  
  
-   Invio di istruzioni SQL per l'origine dati per l'esecuzione. Il driver necessario modificare SQL ODBC per SQL specifici del DBMS. Questo è spesso limitato a sostituendo le clausole di escape definite da ODBC SQL specifici del DBMS.  
  
-   L'invio dei dati e il recupero dei dati dall'origine dati, tra cui la conversione dei tipi di dati come specificato dall'applicazione.  
  
-   Errori specifici del DBMS di mapping di SQLSTATE ODBC.
