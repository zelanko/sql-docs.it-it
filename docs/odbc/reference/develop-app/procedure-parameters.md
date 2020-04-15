---
title: Parametri di procedura Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35d43ca7cf6e603d7dabca9eacf1e026daa753b7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306958"
---
# <a name="procedure-parameters"></a>Parametri di procedure
I parametri nelle chiamate di routine possono essere parametri di input, input/output o output. Questo è diverso dai parametri in tutte le altre istruzioni SQL, che sono sempre parametri di input.  
  
 I parametri di input vengono utilizzati per inviare valori alla procedura. Si supponga, ad esempio, che la tabella Parts abbia le colonne PartID, Description e Price. La routine InsertPart potrebbe avere un parametro di input per ogni colonna della tabella. Ad esempio:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un driver non deve modificare il contenuto di un buffer di input fino a quando **SQLExecDirect** o **SQLExecute** non restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. Il contenuto del buffer di input non deve essere modificato mentre **SQLExecDirect** o **SQLExecute** restituisce SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 I parametri di input/output vengono utilizzati sia per inviare valori alle procedure che per recuperare valori dalle procedure. L'utilizzo dello stesso parametro sia di input che di un parametro di output tende a generare confusione e deve essere evitato. Si supponga, ad esempio, che una procedura accetti un ID ordine e restituisca l'ID del cliente. Questo può essere definito con un singolo parametro di input/output:This can be defined with a single input/output parameter:  
  
```  
{call GetCustID(?)}  
```  
  
 Potrebbe essere preferibile usare due parametri: un parametro di input per l'ID ordine e un parametro di output o input/output per l'ID cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 I parametri di output vengono utilizzati per recuperare il valore restituito della routine e per recuperare i valori dagli argomenti della routine; procedure che restituiscono valori sono talvolta note come *funzioni*. Si supponga, ad esempio, che la routine **GetCustID** appena indicata restituisca un valore che indica se è stato in grado di trovare l'ordine. Nella chiamata seguente, il primo parametro è un parametro di output utilizzato per recuperare il valore restituito della routine, il secondo parametro è un parametro di input utilizzato per specificare l'ID ordine e il terzo parametro è un parametro di output utilizzato per recuperare l'ID cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 I driver gestiscono i valori per i parametri di input e input/output nelle procedure non in modo diverso rispetto ai parametri di input in altre istruzioni SQL. Quando l'istruzione viene eseguita, recuperano i valori delle variabili associate a questi parametri e li inviano all'origine dati.  
  
 Dopo l'esecuzione dell'istruzione, i driver archiviano i valori restituiti dei parametri di input/output e output nelle variabili associate a tali parametri. Questi valori restituiti non è garantito per essere impostati fino a quando tutti i risultati restituiti dalla procedura sono stati recuperati e **SQLMoreResults** ha restituito SQL_NO_DATA. Se l'esecuzione dell'istruzione genera un errore, il contenuto del buffer dei parametri di input/output o del buffer dei parametri di output non è definito.  
  
 Un'applicazione chiama **SQLProcedure** per determinare se una routine ha un valore restituito. Chiama **SQLProcedureColumns** per determinare il tipo (valore restituito, input, input/output o output) di ogni parametro della routine.
