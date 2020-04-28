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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a1e214f50488c4600ed39f76e91618cc5ce53de4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306372"
---
# <a name="binding-parameters-by-name-named-parameters"></a>Associazione di parametri in base al nome (parametri denominati)
Alcuni DBMS consentono a un'applicazione di specificare i parametri per un stored procedure in base al nome invece che in base alla posizione nella chiamata di procedura. Tali parametri sono denominati *parametri denominati*. ODBC supporta l'utilizzo di parametri denominati. In ODBC i parametri denominati vengono utilizzati solo nelle chiamate alle stored procedure e non possono essere utilizzati in altre istruzioni SQL.  
  
 Il driver controlla il valore del campo SQL_DESC_UNNAMED di dpi per determinare se vengono utilizzati i parametri denominati. Se SQL_DESC_UNNAMED non è impostato su SQL_UNNAMED, il driver usa il nome nel campo SQL_DESC_NAME di dpi per identificare il parametro. Per associare il parametro, un'applicazione può chiamare **SQLBindParameter** per specificare le informazioni sui parametri e quindi può chiamare **SQLSetDescField** per impostare il campo SQL_DESC_NAME del dip. Quando si utilizzano parametri denominati, l'ordine del parametro nella chiamata di procedura non è importante e il numero di record del parametro viene ignorato.  
  
 La differenza tra i parametri senza nome e i parametri denominati è la relazione tra il numero di record del descrittore e il numero di parametro nella procedura. Quando si usano parametri senza nome, il primo marcatore di parametro è correlato al primo record nel descrittore del parametro, che a sua volta è correlato al primo parametro (nell'ordine di creazione) nella chiamata di procedura. Quando si utilizzano parametri denominati, il primo marcatore di parametro è ancora correlato al primo record del descrittore del parametro, ma la relazione tra il numero di record del descrittore e il numero di parametro nella procedura non esiste più. I parametri denominati non utilizzano il mapping del numero di record del descrittore alla posizione del parametro della procedura. al contrario, il nome del record del descrittore viene mappato al nome del parametro della procedura.  
  
> [!NOTE]  
>  Se il popolamento automatico del dip è abilitato, il driver compilerà il descrittore in modo che l'ordine dei record del descrittore corrisponda all'ordine dei parametri nella definizione della procedura, anche se vengono usati parametri denominati.  
  
 Se viene utilizzato un parametro denominato, tutti i parametri devono essere denominati parametri. Se un parametro non è un parametro denominato, nessuno dei parametri verrà denominato parametri. Se era presente una combinazione di parametri denominati e parametri senza nome, il comportamento sarebbe dipendente dal driver.  
  
 Come esempio di parametri denominati, si supponga che un SQL Server stored procedure sia stato definito come segue:  
  
```  
CREATE PROCEDURE test @title_id int = 1, @quote char(30) AS <blah>  
```  
  
 In questa procedura, il primo parametro, @title_id, ha un valore predefinito di 1. Un'applicazione può usare il codice seguente per richiamare questa procedura in modo da specificare un solo parametro dinamico. Questo parametro è un parametro denominato con il nome "\@quote".  
  
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
