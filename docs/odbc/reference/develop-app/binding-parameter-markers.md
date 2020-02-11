---
title: Marcatori di parametro di binding | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- parameter markers [ODBC]
- binding parameter markers [ODBC]
ms.assetid: fe88c1c2-4ee4-45e0-8500-b8c25c047815
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0e625e01b9bf4771f18dd8e9807ab09100ca580c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107656"
---
# <a name="binding-parameter-markers"></a>Associazione di marcatori di parametro
L'applicazione associa i parametri chiamando **SQLBindParameter**. **SQLBindParameter** associa un parametro alla volta. Con esso, l'applicazione specifica quanto segue:  
  
-   Numero di parametro. I parametri vengono numerati nell'ordine dei parametri crescente nell'istruzione SQL, a partire dal numero 1. Sebbene sia possibile specificare un numero di parametro superiore al numero di parametri nell'istruzione SQL, il valore del parametro viene ignorato quando viene eseguita l'istruzione.  
  
-   Tipo di parametro (input, input/output o output). Ad eccezione dei parametri nelle chiamate di procedura, tutti i parametri sono parametri di input. Per ulteriori informazioni, vedere [parametri di procedura](../../../odbc/reference/develop-app/procedure-parameters.md)più avanti in questa sezione.  
  
-   Il tipo di dati C, l'indirizzo e la lunghezza in byte della variabile associata al parametro. Il driver deve essere in grado di convertire i dati dal tipo di dati C al tipo di dati SQL oppure viene restituito un errore. Per un elenco delle conversioni supportate, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) in Appendice D: tipi di dati.  
  
-   Il tipo di dati, la precisione e la scala del parametro stesso.  
  
-   Indirizzo di un buffer di lunghezza/indicatore. Fornisce la lunghezza in byte dei dati binari o di tipo carattere, specifica che i dati sono NULL o specifica che i dati verranno inviati con **SQLPutData**. Per ulteriori informazioni, vedere [utilizzo di valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Il codice seguente, ad esempio, associa *venditori* e *CustID* ai parametri per le colonne SalesPerson e custid. Poiché il *venditore* contiene dati di tipo carattere, che è a lunghezza variabile, il codice specifica la lunghezza in byte del *venditore* (11) e associa *SalesPersonLenOrInd* per contenere la lunghezza in byte dei dati nel *venditore*. Queste informazioni non sono necessarie per *CustID* perché contengono dati Integer, a lunghezza fissa.  
  
```  
SQLCHAR       SalesPerson[11];  
SQLINTEGER    SalesPersonLenOrInd, CustIDInd;  
SQLUINTEGER   CustID;  
  
// Bind SalesPerson to the parameter for the SalesPerson column and  
// CustID to the parameter for the CustID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 10, 0,  
                  SalesPerson, sizeof(SalesPerson), &SalesPersonLenOrInd);  
SQLBindParameter(hstmt1, 2, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 10, 0,  
                  &CustID, 0, &CustIDInd);  
  
// Set values of salesperson and customer ID and length/indicators.  
strcpy_s((char*)SalesPerson, _countof(SalesPerson), "Garcia");  
SalesPersonLenOrInd = SQL_NTS;  
CustID = 1331;  
CustIDInd = 0;  
  
// Execute a statement to get data for all orders made to the specified  
// customer by the specified salesperson.  
SQLExecDirect(hstmt1,"SELECT * FROM Orders WHERE SalesPerson=? AND CustID=?",SQL_NTS);  
```  
  
 Quando viene chiamato **SQLBindParameter** , il driver archivia queste informazioni nella struttura per l'istruzione. Quando l'istruzione viene eseguita, vengono utilizzate le informazioni per recuperare i dati del parametro e inviarli all'origine dati.  
  
> [!NOTE]  
>  In ODBC 1,0 i parametri sono associati a **SQLSetParam**. Gestione driver esegue il mapping delle chiamate tra **SQLSetParam** e **SQLBindParameter**, a seconda delle versioni di ODBC utilizzate dall'applicazione e dal driver.
