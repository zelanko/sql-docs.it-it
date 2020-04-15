---
title: Chiamate di routine Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282231"
---
# <a name="procedure-calls"></a>Chiamate di procedura
Una *procedura* è un oggetto eseguibile archiviato nell'origine dati. In genere, si tratta di una o più istruzioni SQL precompilate. La sequenza di escape per chiamare una routine è  
  
 **:**[**?**] ] *nome-routine*[**[***parametro*][**,**[*parametro*]]...**call** **)**]**}**  
  
 dove *nome-procedura* specifica il nome di una routine e *parametro* specifica un parametro di routine.  
  
 Per altre informazioni sulla sequenza di escape delle chiamate di routine, vedere [Sequenza](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) di escape delle chiamate di routine nell'Appendice C: Grammatica SQL.  
  
 Una procedura può avere zero o più parametri. Può anche restituire un valore, come indicato dal marcatore di parametro facoltativo **?** Se *parametro* è un input o un parametro di input/output, può essere un valore letterale o un marcatore di parametro. Tuttavia, le applicazioni interoperabili devono sempre usare gli indicatori di parametro perché alcune origini dati non accettano valori di parametro letterali. Se *parametro* è un parametro di output, deve essere un marcatore di parametro. Gli indicatori di parametro devono essere associati con **SQLBindParameter** prima dell'esecuzione dell'istruzione di chiamata di routine.  
  
 I parametri di input e di input/output possono essere omessi dalle chiamate alle procedure. Se una routine viene chiamata tra parentesi ma senza parametri, ad esempio *nome-routine*di chiamata () , il driver indica all'origine dati di utilizzare il valore predefinito per il primo parametro. Se la procedura non dispone di parametri, è possibile che la procedura abbia esito negativo. Se una routine viene chiamata senza parentesi, ad esempio *nome-routine*di chiamata, il driver non invia alcun valore di parametro.  
  
 È possibile specificare valori letterali per parametri di input e di input/output nelle chiamate alle procedure. Si supponga, ad esempio, che la routine **InsertOrder** disponga di cinque parametri di input. La chiamata seguente a **InsertOrder** omette il primo parametro, fornisce un valore letterale per il secondo parametro e utilizza un marcatore di parametro per il terzo, quarto e quinto parametro:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Si noti che se un parametro viene omesso, la virgola che lo delimita da altri parametri deve comunque essere visualizzata. Se si omette un parametro di input o di input/output, la procedura utilizza il valore predefinito del parametro. Un altro modo per specificare il valore predefinito di un parametro di input o input/output consiste nell'impostare il valore del buffer di lunghezza/indicatore associato al parametro su SQL_DEFAULT_PARAM.  
  
 Se un parametro di input/output viene omesso o se viene fornito un valore letterale per il parametro, il driver elimina il valore di output. Analogamente, se il marcatore di parametro per il valore restituito di una procedura viene omesso, il driver ignora il valore restituito. Se, infine, un'applicazione specifica un parametro di valore restituito per una procedura che non restituisce alcun valore, il driver imposta il valore per il buffer di lunghezza/indicatore associato al parametro su SQL_NULL_DATA.  
  
 Si supponga che la procedura PARTS_IN_ORDERS crea un set di risultati contenente un elenco di ordini che contengono un numero di parte specifico. Il codice seguente chiama questa procedura per il numero di parte 544:  
  
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
  
 Per ulteriori informazioni sulle procedure, vedere [Procedure](../../../odbc/reference/develop-app/procedures-odbc.md).
