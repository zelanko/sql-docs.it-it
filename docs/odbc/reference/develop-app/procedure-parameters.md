---
title: I parametri di routine | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cab0fea9c39e4946122698f2476668464e556c1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861531"
---
# <a name="procedure-parameters"></a>Parametri di procedure
I parametri nelle chiamate a procedure possono essere di input, input/output o i parametri di output. Questo è diverso dai parametri di tutte le altre istruzioni di SQL, che sono sempre i parametri di input.  
  
 I parametri di input vengono utilizzati per inviare i valori per la procedura. Si supponga, ad esempio, che la tabella di parti contiene colonne PartID, la descrizione e prezzo. La routine InsertPart può avere un parametro di input per ogni colonna nella tabella. Ad esempio:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un driver non deve modificare il contenuto di un buffer di input fino alla **SQLExecDirect** oppure **SQLExecute** restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. Il contenuto del buffer di input non deve essere modificato mentre **SQLExecDirect** oppure **SQLExecute** restituisce SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 Parametri di input/output vengono utilizzati sia per inviare i valori per le procedure e recuperare i valori da routine. Usando lo stesso parametro come input e un parametro di output tende a generare confusione e deve essere evitata. Si supponga, ad esempio, una procedura accetta un ID ordine e restituisce l'ID del cliente. Ciò può essere definito con un singolo parametro di input/output:  
  
```  
{call GetCustID(?)}  
```  
  
 Potrebbe essere preferibile usare due parametri: un parametro di input per l'ID dell'ordine e un output o un parametro di input/output per l'ID cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 I parametri di output vengono usati per recuperare il valore restituito di routine e per recuperare valori da argomenti di procedure. le procedure che restituiscono i valori vengono talvolta nota anche come *funzioni*. Ad esempio, si supponga che il **GetCustID** procedure descritti in precedenza restituisce un valore che indica se è stato possibile trovare l'ordine. Nella chiamata seguente, il primo parametro è un parametro di output usato per recuperare il valore restituito di routine, il secondo parametro è un parametro di input utilizzato per specificare l'ID dell'ordine e il terzo parametro è un parametro di output usato per recuperare l'ID cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 I driver di gestiscono i valori per l'input, input/output parametri nelle procedure no in modo diverso rispetto ai parametri di input in altre istruzioni SQL. Quando viene eseguita l'istruzione, vengano recuperati i valori delle variabili associate a questi parametri e inviarli all'origine dati.  
  
 Dopo l'istruzione è stata eseguita, i driver di archiviano i valori restituiti di input/output e i parametri di output nelle variabili associate a tali parametri. Questi ha restituito valori non sono garantiti da impostare fino a dopo che sono stati recuperati tutti i risultati restituiti dalla procedura e **SQLMoreResults** è stato restituito SQL_NO_DATA. Se l'esecuzione dell'istruzione genera un errore, il contenuto del buffer del parametro di input/output o buffer dei parametri di output è definito.  
  
 Un'applicazione chiama **SQLProcedure** per determinare se una procedura con un valore restituito. Viene chiamato **SQLProcedureColumns** per determinare il tipo (valore restituito, input, input/output o di output) di ogni parametro di routine.
