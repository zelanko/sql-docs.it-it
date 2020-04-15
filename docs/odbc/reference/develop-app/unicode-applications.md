---
title: Proprietà Unicode Applications Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298947"
---
# <a name="unicode-applications"></a>Applicazioni Unicode
È possibile ricompilare un'applicazione come applicazione Unicode in uno dei due modi seguenti:You can recompile an application as a Unicode application in one of two ways:  
  
-   Includere il **#define** Unicode contenuto nel file di intestazione Sqlucode.h nell'applicazione.  
  
-   Compilare l'applicazione con l'opzione Unicode del compilatore. (Questa opzione sarà diversa per i diversi compilatori.)  
  
 Per convertire un'applicazione ANSI in un'applicazione Unicode, scrivere l'applicazione per archiviare e passare i dati Unicode. Inoltre, le chiamate alle funzioni che supportano gli argomenti SQLPOINTER devono essere convertite per utilizzare il conteggio dei byte.  
  
 Dopo che un'applicazione viene compilata come un'applicazione Unicode, se l'applicazione chiama una funzione API ODBC (senza suffisso), Gestione Driver riconosce l'applicazione come un'applicazione Unicode e converte la chiamata di funzione in una funzione Unicode (con il suffisso *W)* se il driver sottostante supporta Unicode. Quando un'applicazione ANSI effettua una chiamata di funzione senza un suffisso, Gestione Driver converte in ANSI se il driver sottostante supporta ANSI. Se sia l'applicazione che il driver supportano la stessa codifica dei caratteri, Gestione driver passa le chiamate al driver (con alcune eccezioni per le applicazioni ANSI).  
  
 Un'applicazione può chiamare entrambe le funzioni Unicode (con il suffisso *W)* e le funzioni ANSI (con o senza il suffisso *A).* Le chiamate di funzione Unicode e ANSI possono essere mescolate. Se la libreria di cursori deve essere utilizzata, tuttavia, le chiamate di funzione Unicode e ANSI non possono essere mescolate. La libreria di cursori è Unicode o ANSI, non una combinazione.  
  
 Un'applicazione può essere scritta in modo che possa essere compilata come un'applicazione Unicode o un'applicazione ANSI. In questo caso, i tipi di dati carattere possono essere dichiarati come SQL_C_TCHAR. Si tratta di una macro che inserisce SQL_C_WCHAR se l'applicazione viene compilata come un'applicazione Unicode o inserisce SQL_C_CHAR se viene compilata come applicazione ANSI. Il programmatore dell'applicazione deve prestare attenzione alle funzioni che accettano SQLPOINTER come argomento, perché la dimensione dell'argomento length cambierà (per i tipi di dati stringa) a seconda che l'applicazione sia ANSI o Unicode.  
  
 Una funzione può essere chiamata in uno dei tre modi seguenti: come chiamata di funzione solo Unicode (con il suffisso *W),* come chiamata di funzione solo ANSI (con il suffisso *A)* o come chiamata di funzione ODBC senza suffisso. Gli argomenti delle tre forme di una funzione sono identici. Solo le funzioni \* con argomenti SQLCHAR o SQLPOINTER che puntano a stringhe richiedono formati Unicode e ANSI. Per le funzioni che dispongono di argomenti che possono essere dichiarati come tipo di carattere, ad esempio **SQLBindCol** o **SQLGetData** (che non dispongono di formati Unicode e ANSI), l'argomento può essere dichiarato come tipo Unicode, tipo ANSI o, nel caso di un argomento di tipo C, la macro SQL_C_TCHAR. Per ulteriori informazioni, vedere [Dati Unicode](../../../odbc/reference/develop-app/unicode-data.md).  
  
 Un'applicazione può essere scritta come applicazione Unicode anche se non sono disponibili driver Unicode per l'utilizzo. Gestione Driver esederà il mapping di funzioni Unicode e tipi di dati ANSI. Esistono alcune restrizioni ai mapping da Unicode a ANSI che possono essere eseguite. L'esistenza di un driver Unicode per l'applicazione Unicode da utilizzare comporterà prestazioni migliori e rimuoverà le restrizioni inerenti ai mapping da Unicode ad ANSI.
