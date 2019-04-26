---
title: Applicazioni Unicode | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Unicode [ODBC], compiling as Unicode application
- Unicode [ODBC], functions
- compiling Unicode applications [ODBC]
- functions [ODBC], Unicode functions
ms.assetid: 7986c623-2792-4e77-bfee-c86cbf84f08d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fc9cb98837d206d5279d1f14d4a57ce56782759
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633381"
---
# <a name="unicode-applications"></a>Applicazioni Unicode
È possibile ricompilare un'applicazione come un'applicazione Unicode in uno dei due modi:  
  
-   Includere Unicode **#define** contenute nel file di intestazione sqlucode nell'applicazione.  
  
-   Compilare l'applicazione con l'opzione del compilatore Unicode. (Questa opzione sarà diversa per diversi compilatori.)  
  
 Per convertire un'applicazione ANSI in Unicode, scrivere l'applicazione per archiviare e passare i dati Unicode. Inoltre, le chiamate alle funzioni che supportano gli argomenti SQLPOINTER devono essere convertite per utilizzare il numero di byte.  
  
 Dopo che un'applicazione viene compilata come un'applicazione Unicode, se l'applicazione chiama una funzione API ODBC (senza un suffisso), gestione Driver riconosce l'applicazione come un'applicazione Unicode e converte la chiamata di funzione a una funzione Unicode (con il  *W* suffisso) se il driver sottostante supporta Unicode. Quando un'applicazione ANSI esegue una funzione chiamate senza un suffisso, gestione Driver lo converte in ANSI se il driver sottostante supporta ANSI. Se l'applicazione e il driver supporta la stessa codifica dei caratteri, Gestione driver passa le chiamate tramite il driver (con alcune eccezioni per le applicazioni ANSI).  
  
 Un'applicazione può chiamare entrambe le funzioni Unicode (con il *W* suffisso) e funzioni ANSI (con o senza il *oggetto* suffisso). È possibile combinare le chiamate di funzione ANSI e Unicode. Se viene utilizzata la libreria di cursori, tuttavia, le chiamate di funzione Unicode e ANSI non possono essere combinate. La libreria di cursori è un valore Unicode o ANSI, non usare una combinazione.  
  
 Un'applicazione può essere scritta in modo che può essere compilato come un'applicazione Unicode o come applicazioni ANSI. In questo caso, i tipi di dati carattere possono essere dichiarati come SQL_C_TCHAR. Si tratta di una macro che inserisce SQL_C_WCHAR se l'applicazione viene compilata come un'applicazione Unicode oppure ne inserisce SQL_C_CHAR se viene compilato come applicazioni ANSI. Il programmatore di applicazioni deve essere un'attenta delle funzioni che accettano SQLPOINTER come argomento, poiché le dimensioni dell'argomento length cambierà (per i tipi di dati stringa) a seconda che l'applicazione sia ANSI o Unicode.  
  
 Una funzione può essere chiamata in uno dei tre modi: come una chiamata di funzione solo Unicode (con il *W* suffisso), come una chiamata di funzione solo ANSI (con il *oggetto* suffisso), o come chiamata di funzione ODBC senza alcun suffisso. Gli argomenti per le tre forme di una funzione sono identici. Solo le funzioni con SQLCHAR \* argomenti o argomenti SQLPOINTER che puntano alle stringhe richiedono form Unicode e ANSI. Per le funzioni con argomenti che possono essere dichiarati come tipo di carattere, ad esempio **SQLBindCol** oppure **SQLGetData** (che non hanno formati ANSI e Unicode), l'argomento può essere dichiarato come tipo di Unicode, ANSI digitare oppure nel caso di C argomento, la macro SQL_C_TCHAR. Per altre informazioni, vedere [dati Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Un'applicazione può essere scritta come un'applicazione Unicode, anche se non sono disponibili per farli funzionare con i driver Unicode. Gestione Driver verrà eseguito il mapping tipi di dati e le funzioni Unicode ad ANSI. Esistono alcune restrizioni per la versione Unicode ai mapping ANSI che possono essere eseguite. L'esistenza di un driver di Unicode per l'applicazione di Unicode lavorare con comporterà prestazioni migliori e rimuoverà le limitazioni intrinseche in Unicode per il mapping ANSI.
