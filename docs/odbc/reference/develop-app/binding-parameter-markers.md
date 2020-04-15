---
title: Indicatori di parametro di associazione . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be99bc884a8baa66f3d632ee4731985f0cc85732
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306392"
---
# <a name="binding-parameter-markers"></a>Associazione di marcatori di parametro
L'applicazione associa i parametri chiamando **SQLBindParameter**. **SQLBindParameter** associa un parametro alla volta. Con esso, l'applicazione specifica quanto segue:  
  
-   Numero del parametro. I parametri sono numerati in ordine crescente nell'istruzione SQL, a partire dal numero 1. Sebbene sia utile specificare un numero di parametro superiore al numero di parametri nell'istruzione SQL, il valore del parametro verrà ignorato quando viene eseguita l'istruzione.  
  
-   Il tipo di parametro (input, input/output o output). Ad eccezione dei parametri nelle chiamate di routine, tutti i parametri sono parametri di input. Per ulteriori informazioni, vedere [Parametri di routine](../../../odbc/reference/develop-app/procedure-parameters.md)più avanti in questa sezione.  
  
-   Il tipo di dati C, l'indirizzo e la lunghezza in byte della variabile associata al parametro. Il driver deve essere in grado di convertire i dati dal tipo di dati C al tipo di dati SQL o viene restituito un errore. Per un elenco delle conversioni supportate, vedere [Conversione](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) di dati da C a tipi di dati SQL nell'Appendice D: tipi di dati.  
  
-   Tipo di dati SQL, precisione e scala del parametro stesso.  
  
-   Indirizzo di un buffer di lunghezza/indicatore. Fornisce la lunghezza in byte dei dati binari o di tipo carattere, specifica che i dati sono NULL o specifica che i dati verranno inviati con **SQLPutData**. Per ulteriori informazioni, consultate [Utilizzo dei valori di lunghezza/indicatore.](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
 Ad esempio, il codice seguente associa *SalesPerson* e *CustID* ai parametri per le colonne SalesPerson e CustID. Poiché *SalesPerson* contiene dati di tipo carattere, ovvero lunghezza variabile, il codice specifica la lunghezza in byte di *SalesPerson* (11) e associa *SalesPersonLenOrInd* per contenere la lunghezza in byte dei dati in *SalesPerson*. Queste informazioni non sono necessarie per *CustID* perché contengono dati interi, che sono di lunghezza fissa.  
  
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
  
 Quando **SQLBindParameter** viene chiamato, il driver archivia queste informazioni nella struttura per l'istruzione. Quando l'istruzione viene eseguita, utilizza le informazioni per recuperare i dati del parametro e inviarli all'origine dati.  
  
> [!NOTE]  
>  In ODBC 1.0 i parametri erano associati a **SQLSetParam**. Gestione Driver esegue il mapping delle chiamate tra **SQLSetParam** e **SQLBindParameter**, a seconda delle versioni di ODBC utilizzate dall'applicazione e dal driver.
