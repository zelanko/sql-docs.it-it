---
title: Parametri di associazione in base al nome (parametri denominati) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- named parameters [ODBC]
- binding parameters by name [ODBC]
ms.assetid: e2c3da5a-6c10-4dd5-acf9-e951eea71a6b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306372"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Associazione di parametri in base al nome (parametri denominati)
Alcuni DBSMO consentono a un'applicazione di specificare i parametri di una stored procedure in base al nome anziché in base alla posizione nella chiamata di routine. Tali parametri sono denominati *parametri denominati*. ODBC supporta l'utilizzo di parametri denominati. In ODBC i parametri denominati vengono utilizzati solo nelle chiamate alle stored procedure e non possono essere utilizzati in altre istruzioni SQL.  
  
 Il driver controlla il valore del campo SQL_DESC_UNNAMED dell'IPD per determinare se vengono utilizzati parametri denominati. Se SQL_DESC_UNNAMED non è impostato su SQL_UNNAMED, il driver utilizza il nome nel campo SQL_DESC_NAME dell'IPD per identificare il parametro. Per associare il parametro, un'applicazione può chiamare **SQLBindParameter** per specificare le informazioni sul parametro e quindi chiamare **SQLSetDescField** per impostare il campo SQL_DESC_NAME dell'IPD. Quando vengono utilizzati parametri denominati, l'ordine del parametro nella chiamata di routine non è importante e il numero di record del parametro viene ignorato.  
  
 La differenza tra parametri senza nome e parametri denominati è nella relazione tra il numero di record del descrittore e il numero di parametro nella procedura. Quando vengono utilizzati parametri senza nome, il primo indicatore di parametro è correlato al primo record nel descrittore di parametro, che a sua volta è correlato al primo parametro (nell'ordine di creazione) nella chiamata di routine. Quando vengono utilizzati parametri denominati, il primo marcatore di parametro è ancora correlato al primo record del descrittore di parametro, ma la relazione tra il numero di record del descrittore e il numero di parametro nella procedura non esiste più. I parametri denominati non utilizzano il mapping del numero di record del descrittore alla posizione del parametro della routine. al nome del parametro della routine viene invece eseguito il mapping del nome del record del descrittore.  
  
> [!NOTE]  
>  Se il popolamento automatico dell'IPD è abilitato, il driver popolerà il descrittore in modo che l'ordine dei record del descrittore corrisponda all'ordine dei parametri nella definizione della procedura, anche se vengono utilizzati parametri denominati.  
  
 Se viene utilizzato un parametro denominato, tutti i parametri devono essere parametri denominati. Se un parametro non è un parametro denominato, nessuno dei parametri può essere denominato parametri. Se esistesse una combinazione di parametri denominati e parametri senza nome, il comportamento sarebbe dipendente dal driver.  
  
 Come esempio di parametri denominati, si supponga che una stored procedure di SQL Server sia stata definita come segue:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 In questa procedura, il @title_idprimo parametro, , ha un valore predefinito pari a 1. Un'applicazione può utilizzare il codice seguente per richiamare questa procedura in modo che specifichi un solo parametro dinamico. Questo parametro è un parametro denominato con il nome "\@quote ".  
  
```  
// Prepare the procedure invocation statement.  
SQLPrepare(hstmt, "{call test(?)}", SQL_NTS);  
  
// Populate record 1 of ipd.  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR,  
                  30, 0, szQuote, 0, &cbValue);  
  
// Get ipd handle and set the SQL_DESC_NAMED and SQL_DESC_UNNAMED fields  
// for record #1.  
SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
// Assuming that szQuote has been appropriately initialized,  
// execute.  
SQLExecute(hstmt);  
```
