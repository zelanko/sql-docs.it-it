---
title: Parametri di procedura | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306958"
---
# <a name="procedure-parameters"></a>Parametri di procedure
I parametri nelle chiamate di routine possono essere parametri di input, di input/output o di output. Si tratta di parametri diversi da quelli presenti in tutte le altre istruzioni SQL, che sono sempre parametri di input.  
  
 I parametri di input vengono utilizzati per inviare valori alla procedura. Si supponga, ad esempio, che la tabella Parts includa le colonne PartID, Description e price. La procedura InsertPart potrebbe avere un parametro di input per ogni colonna della tabella. Ad esempio:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un driver non deve modificare il contenuto di un buffer di input fino a quando **SQLExecDirect** o **SQLExecute** non restituisce SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. Il contenuto del buffer di input non deve essere modificato mentre **SQLExecDirect** o **sqlexecute** restituisce SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 I parametri di input/output vengono utilizzati sia per inviare valori a procedure che per recuperare valori dalle routine. L'uso dello stesso parametro di un parametro di input e di output tende a essere confuso e deve essere evitato. Si supponga, ad esempio, che una routine accetti un ID ordine e restituisca l'ID del cliente. Questo può essere definito con un singolo parametro di input/output:  
  
```  
{call GetCustID(?)}  
```  
  
 Potrebbe essere preferibile usare due parametri: un parametro di input per l'ID dell'ordine e un parametro di output o di input/output per l'ID cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 I parametri di output vengono utilizzati per recuperare il valore restituito della procedura e recuperare i valori dagli argomenti della routine. le routine che restituiscono valori sono talvolta note come *funzioni*. Si supponga, ad esempio, che la procedura **GetCustID** appena citata restituisca un valore che indica se è stato in grado di trovare l'ordine. Nella chiamata seguente il primo parametro è un parametro di output utilizzato per recuperare il valore restituito della procedura, il secondo parametro è un parametro di input utilizzato per specificare l'ID dell'ordine e il terzo parametro è un parametro di output utilizzato per recuperare l'ID cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 I driver gestiscono i valori per i parametri di input e di input/output nelle procedure in modo diverso rispetto ai parametri di input in altre istruzioni SQL. Quando l'istruzione viene eseguita, recupera i valori delle variabili associato a questi parametri e li invia all'origine dati.  
  
 Al termine dell'esecuzione dell'istruzione, i driver archiviano i valori restituiti dei parametri di input/output e di output nelle variabili che delegano a tali parametri. Non è garantito che i valori restituiti vengano impostati fino a quando tutti i risultati restituiti dalla stored procedure non sono stati recuperati e **SQLMoreResults** ha restituito SQL_NO_DATA. Se l'esecuzione dell'istruzione genera un errore, il contenuto del buffer del parametro di input/output o del buffer dei parametri di output non è definito.  
  
 Un'applicazione chiama **SqlProcedure** per determinare se una stored procedure ha un valore restituito. Chiama **SQLProcedureColumns** per determinare il tipo (valore restituito, input, input/output o output) di ogni parametro di procedura.
