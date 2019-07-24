---
title: Le chiamate di procedura | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 926ee91fae207d50248df4c82d1b82bb6424e239
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023248"
---
# <a name="procedure-calls"></a>Chiamate di procedura
Oggetto *procedure* è un oggetto eseguibile archiviato nell'origine dati. In genere, si tratta di una o più istruzioni SQL precompilate. La sequenza di escape per chiamare una routine  
  
 **{** [ **? =** ]**chiamare** *nome procedura*[ **(** [*parametro*] [ **,** [*parametro*]]... **)** ] **}**  
  
 in cui *-nome della routine* specifica il nome di una stored procedure e *parametro* specifica un parametro di routine.  
  
 Per altre informazioni sulla sequenza di escape chiamata di procedura, vedere [procedura sequenza di Escape Call](../../../odbc/reference/appendixes/procedure-call-escape-sequence.md) nell'appendice c: Grammatica SQL.  
  
 Una procedura può avere zero o più parametri. Può inoltre restituire un valore, come indicato dall'indicatore di parametro facoltativo **? =** all'inizio della sintassi. Se *parametro* è un input o un parametro di input/output può essere un valore letterale o un marcatore di parametro. Tuttavia, applicazioni interoperative devono usare sempre i marcatori di parametro poiché alcune origini dati non accetta i valori dei parametri di valore letterale. Se *parametro* è un parametro di output deve essere un marcatore di parametro. Marcatori di parametro devono essere associati con **SQLBindParameter** prima della chiamata di procedura viene eseguita l'istruzione.  
  
 I parametri di input e di input/output possono essere omessi dalle chiamate alle procedure. Se una routine viene chiamata con parentesi ma senza parametri, ad esempio {chiamare *-nome della routine*()}, il driver indica all'origine dati per utilizzare il valore predefinito per il primo parametro. Se la procedura non ha alcun parametro, ciò potrebbe causare la procedura per avere esito negativo. Se una routine viene chiamata senza parentesi, ad esempio {chiamare *-nome della routine*}, il driver non invia i valori dei parametri.  
  
 È possibile specificare valori letterali per parametri di input e di input/output nelle chiamate alle procedure. Ad esempio, si supponga che la procedura **InsertOrder** include cinque parametri di input. La chiamata seguente a **InsertOrder** omette il primo parametro, fornisce un valore letterale per il secondo parametro e utilizza un marcatore di parametro per il terzo, quarto e quinto parametri:  
  
```  
{call InsertOrder(, 10, ?, ?, ?)}   // Not interoperable!  
```  
  
 Si noti che se un parametro viene omesso, la virgola che lo delimita rispetto ad altri parametri deve comunque essere presente. Se si omette un parametro di input o di input/output, la procedura utilizza il valore predefinito del parametro. Un altro modo per specificare che il valore predefinito di un parametro di input o input/output consiste nell'impostare il valore del buffer di lunghezza/indicatore associato al parametro su SQL_DEFAULT_PARAM.  
  
 Se si omette un parametro di input/output o se un valore letterale viene fornito per il parametro, il driver ignora il valore di output. Analogamente, se il marcatore di parametro per il valore restituito di una procedura viene omesso, il driver ignora il valore restituito. Se, infine, un'applicazione specifica un parametro di valore restituito per una procedura che non restituisce alcun valore, il driver imposta il valore per il buffer di lunghezza/indicatore associato al parametro su SQL_NULL_DATA.  
  
 Si supponga che la procedura PARTS_IN_ORDERS crea un set di risultati che contiene un elenco di ordini che contengono un numero specifico. Il codice seguente chiama questa procedura per il numero di parte 544:  
  
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
  
 Per determinare se un'origine dati supporta la routine, un'applicazione chiama **SQLGetInfo** con l'opzione SQL_PROCEDURES.  
  
 Per altre informazioni sulle procedure, vedere [procedure](../../../odbc/reference/develop-app/procedures-odbc.md).
