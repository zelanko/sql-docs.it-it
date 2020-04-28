---
title: Chiamate di routine | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure calls
- procedure calls [ODBC]
ms.assetid: 145130cc-40e7-4722-8417-dff131084752
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9c52e72512c8b81c6872461207f235ea2731ac5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81282231"
---
# <a name="procedure-calls"></a>Chiamate di procedura
Una *routine* è un oggetto eseguibile archiviato nell'origine dati. In genere, si tratta di una o più istruzioni SQL precompilate. La sequenza di escape per la chiamata di una stored procedure è  
  
 **{**[**? =**]**Call** *-routine-nome*[**(**[*parametro*] [**,**[*parametro*]]... **)**]**}**  
  
 dove *procedure-name* specifica il nome di una routine e il *parametro* specifica un parametro di routine.  
  
 Per ulteriori informazioni sulla sequenza di escape della chiamata di procedura, vedere [sequenza di escape della chiamata di procedura](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) nell'Appendice C: grammatica SQL.  
  
 Una procedura può avere zero o più parametri. Può anche restituire un valore, come indicato dal marcatore di parametro facoltativo **? =** all'inizio della sintassi. Se il *parametro* è un parametro di input o di input/output, può essere un valore letterale o un marcatore di parametro. Tuttavia, le applicazioni interoperative devono sempre usare i marcatori di parametro perché alcune origini dati non accettano valori di parametri letterali. Se il *parametro* è un parametro di output, deve essere un marcatore di parametro. I marcatori di parametro devono essere associati con **SQLBindParameter** prima dell'esecuzione dell'istruzione di chiamata di procedura.  
  
 I parametri di input e di input/output possono essere omessi dalle chiamate alle procedure. Se una stored procedure viene chiamata con le parentesi ma senza parametri, ad esempio {Call *procedure-name*()}, il driver indica all'origine dati di usare il valore predefinito per il primo parametro. Se la routine non dispone di parametri, è possibile che la procedura abbia esito negativo. Se una procedura viene chiamata senza parentesi, ad esempio {Call *procedure-name*}, il driver non invia alcun valore di parametro.  
  
 È possibile specificare valori letterali per parametri di input e di input/output nelle chiamate alle procedure. Si supponga, ad esempio, che la stored procedure **InsertOrder** includa cinque parametri di input. La chiamata seguente a **InsertOrder** omette il primo parametro, fornisce un valore letterale per il secondo parametro e usa un marcatore di parametro per i parametri terzo, quarto e quinto:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Si noti che se un parametro viene omesso, la virgola che lo delimita da altri parametri deve comunque essere visualizzata. Se si omette un parametro di input o di input/output, la procedura utilizza il valore predefinito del parametro. Un altro modo per specificare il valore predefinito di un parametro di input o di input/output consiste nell'impostare il valore del buffer di lunghezza/indicatore associato al parametro su SQL_DEFAULT_PARAM.  
  
 Se un parametro di input/output viene omesso o se viene specificato un valore letterale per il parametro, il driver ignora il valore di output. Analogamente, se il marcatore di parametro per il valore restituito di una procedura viene omesso, il driver ignora il valore restituito. Se, infine, un'applicazione specifica un parametro di valore restituito per una procedura che non restituisce alcun valore, il driver imposta il valore per il buffer di lunghezza/indicatore associato al parametro su SQL_NULL_DATA.  
  
 Si supponga che la procedura PARTS_IN_ORDERS crei un set di risultati contenente un elenco di ordini che contengono un determinato numero di parte. Il codice seguente chiama questa procedura per il numero di parte 544:  
  
```  
SQLUINTEGER   PartID;  
SQLINTEGER    PartIDInd = 0;  
  
// Bind the parameter.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_SLONG, SQL_INTEGER, 0, 0,  
                  &PartID, 0, PartIDInd);  
  
// Place the department number in PartID.  
PartID = 544;  
  
// Execute the statement.  
SQLExecDirect(hstmt, "{call PARTS_IN_ORDERS(?)}", SQL_NTS);  
```  
  
 Per determinare se un'origine dati supporta le procedure, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_PROCEDURES.  
  
 Per ulteriori informazioni sulle procedure, vedere [procedure](../../../odbc/reference/develop-app/procedures-odbc.md).
