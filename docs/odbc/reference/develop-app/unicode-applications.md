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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 94bd5211c878904453624adb2acd0fe435ebc812
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298947"
---
# <a name="unicode-applications"></a>Applicazioni Unicode
È possibile ricompilare un'applicazione come applicazione Unicode in uno dei due modi seguenti:  
  
-   Includere il **#define** Unicode contenuto nel file di intestazione Sqlucode. h nell'applicazione.  
  
-   Compilare l'applicazione con l'opzione Unicode del compilatore. Questa opzione sarà diversa per i diversi compilatori.  
  
 Per convertire un'applicazione ANSI in un'applicazione Unicode, scrivere l'applicazione in modo da archiviare e passare i dati Unicode. Inoltre, le chiamate alle funzioni che supportano gli argomenti SQLPOINTER devono essere convertite in modo da utilizzare il conteggio di byte.  
  
 Quando un'applicazione viene compilata come applicazione Unicode, se l'applicazione chiama una funzione API ODBC (senza suffisso), gestione driver riconosce l'applicazione come applicazione Unicode e converte la chiamata di funzione in una funzione Unicode (con il suffisso *W* ) se il driver sottostante supporta Unicode. Quando un'applicazione ANSI esegue una chiamata di funzione senza un suffisso, gestione driver la converte in ANSI se il driver sottostante supporta ANSI. Se sia l'applicazione che il driver supportano la stessa codifica dei caratteri, gestione driver passa le chiamate al driver (con determinate eccezioni per le applicazioni ANSI).  
  
 Un'applicazione può chiamare sia funzioni Unicode (con il suffisso *W* ) che funzioni ANSI (con o senza il suffisso *a* ). Le chiamate di funzione Unicode e ANSI possono essere combinate. Se è necessario utilizzare la libreria di cursori, tuttavia, non è possibile combinare le chiamate di funzione Unicode e ANSI. La libreria di cursori può essere Unicode o ANSI, non una combinazione.  
  
 È possibile scrivere un'applicazione in modo che possa essere compilata come applicazione Unicode o come applicazione ANSI. In questo caso, i tipi di dati character possono essere dichiarati come SQL_C_TCHAR. Si tratta di una macro che inserisce SQL_C_WCHAR se l'applicazione viene compilata come applicazione Unicode o inserisce SQL_C_CHAR se viene compilata come applicazione ANSI. Il programmatore di applicazioni deve prestare attenzione alle funzioni che accettano SQLPOINTER come argomento, perché la dimensione dell'argomento length cambierà (per i tipi di dati stringa) a seconda che l'applicazione sia ANSI o Unicode.  
  
 Una funzione può essere chiamata in uno dei tre modi seguenti: come chiamata di funzione solo Unicode (con il suffisso *W* ), come chiamata di funzione solo ANSI (con il suffisso *a* ) o come chiamata di funzione ODBC senza suffisso. Gli argomenti per le tre forme di una funzione sono identici. Solo le funzioni con argomenti SQLCHAR \* o argomenti SQLPOINTER che puntano a stringhe richiedono form Unicode e ANSI. Per le funzioni con argomenti che possono essere dichiarati come tipo di carattere, ad esempio **SQLBindCol** o **SQLGetData** (che non hanno form Unicode e ANSI), l'argomento può essere dichiarato come tipo Unicode, tipo ANSI o nel caso di un argomento di tipo C, la SQL_C_TCHAR macro. Per ulteriori informazioni, vedere [dati Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Un'applicazione può essere scritta come applicazione Unicode anche se non sono disponibili driver Unicode per l'utilizzo. Gestione driver eseguirà il mapping di funzioni e tipi di dati Unicode a ANSI. Esistono alcune restrizioni per i mapping Unicode ai mapping ANSI che è possibile eseguire. L'esistenza di un driver Unicode per l'applicazione Unicode con può comportare prestazioni migliori e rimuoverà le restrizioni inerenti i mapping Unicode ai mapping ANSI.
