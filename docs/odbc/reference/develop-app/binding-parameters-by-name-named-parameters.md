---
title: Associazione di parametri in base al nome (parametri denominati) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68dfb8976312016ee7f2e42fc4fcdecb93fd28cf
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199372"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Associazione di parametri in base al nome (parametri denominati)
Determinati DBMS consente di specificare i parametri da una stored procedure in base al nome anziché in base alla posizione nella chiamata di procedura. Tali parametri vengono chiamati *parametri denominati*. ODBC supporta l'utilizzo di parametri denominati. In ODBC, i parametri denominati sono utilizzati solo nelle chiamate alle stored procedure e non possono essere utilizzati in altre istruzioni SQL.  
  
 Il driver controlla il valore del campo SQL_DESC_UNNAMED dell'IPD per determinare se denominato vengono utilizzati i parametri. Se SQL_DESC_UNNAMED non è impostata su SQL_UNNAMED, il driver Usa il nome nel campo SQL_DESC_NAME dell'IPD per identificare il parametro. Per associare il parametro, un'applicazione può chiamare **SQLBindParameter** per specificare le informazioni sul parametro e quindi possibile chiamare **SQLSetDescField** per impostare il campo SQL_DESC_NAME dell'IPD. Quando si utilizzano parametri denominati, non è importante l'ordine del parametro nella chiamata di procedura e numero di record del parametro viene ignorato.  
  
 La differenza tra i parametri denominati e i parametri senza nome è la relazione tra il numero di record del descrittore e il numero di parametri nella procedura. Quando si utilizzano parametri senza nome, il primo marcatore di parametro è correlato al primo record nel descrittore del parametro, che a sua volta è correlato al primo parametro (in ordine di creazione) nella chiamata di procedura. Quando si utilizzano parametri denominati, il primo marcatore di parametro è ancora correlato al primo record del descrittore del parametro, ma la relazione tra il numero del parametro nella procedura e il numero di record del descrittore non esiste più. I parametri denominati non utilizzano il mapping del numero di record del descrittore per la posizione del parametro procedura; al contrario, il nome del record del descrittore viene eseguito il mapping al nome di parametro della procedura.  
  
> [!NOTE]  
>  Se il popolamento automatico dell'IPD è abilitato, il driver popolerà il descrittore di modo che l'ordine dei record del descrittore corrisponderà all'ordine dei parametri nella definizione della routine, anche se si utilizzano parametri denominati.  
  
 Se viene usato un parametro denominato, tutti i parametri devono essere parametri denominati. Se qualsiasi parametro non è un parametro denominato, quindi nessuna delle autorità di certificazione parametri denominate parametri. Se si sono una combinazione di parametri denominati e i parametri senza nome, il comportamento sarà dipendente dal driver.  
  
 Ad esempio di parametri denominati, si supponga che un Server SQL stored procedure è stata definita come segue:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 In questa procedura, il primo parametro, @title_id, ha un valore predefinito pari a 1. Un'applicazione può usare il codice seguente per richiamare questa procedura in modo che specifichi un solo parametro dinamico. Questo parametro è un parametro denominato con il nome "\@offerta".  
  
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
