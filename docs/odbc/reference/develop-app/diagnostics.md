---
description: Diagnostica
title: Diagnostica | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC]
- functions [ODBC], diagnostic information
- diagnostic information [ODBC], about diagnostic information
ms.assetid: 450abd88-90a1-4fbc-b417-8efbdd8e1dea
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 918dce41ca1c7e7b43c1a6d25de2c75a83312715
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476713"
---
# <a name="diagnostics"></a>Diagnostica
Le funzioni in ODBC restituiscono informazioni di diagnostica in due modi. Il codice restituito indica l'esito positivo o negativo complessivo della funzione, mentre i record di diagnostica forniscono informazioni dettagliate sulla funzione. Almeno un record di diagnostica, ovvero il record di intestazione, viene restituito anche se la funzione ha esito positivo.  
  
 Le informazioni di diagnostica vengono utilizzate in fase di sviluppo per rilevare errori di programmazione, ad esempio handle non validi ed errori di sintassi nelle istruzioni SQL hardcoded. Viene utilizzato in fase di esecuzione per rilevare errori di run-time e avvisi quali il troncamento dei dati, le violazioni di accesso e gli errori di sintassi nelle istruzioni SQL immesse dall'utente.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Codici restituiti](../../../odbc/reference/develop-app/return-codes-odbc.md)  
  
-   [Record di diagnostica](../../../odbc/reference/develop-app/diagnostic-records.md)  
  
-   [Uso di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Implementazione di SQLGetDiagRec e SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md)  
  
-   [Esempi di gestione di diagnostica](../../../odbc/reference/develop-app/diagnostic-handling-examples.md)
