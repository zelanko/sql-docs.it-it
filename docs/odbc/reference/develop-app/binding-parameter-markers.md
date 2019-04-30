---
title: Marcatori di parametro di associazione | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: c71967bd72f7f13a725d47517cb9e66eee7da87f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199390"
---
# <a name="binding-parameter-markers"></a>Associazione di marcatori di parametro
L'applicazione associa parametri chiamando **SQLBindParameter**. **SQLBindParameter** associa un parametro alla volta. In tal modo l'applicazione specifica quanto segue:  
  
-   Il numero di parametro. I parametri sono numerati in ordine crescente dei parametri nell'istruzione SQL, a partire dal numero 1. Anche se è consentito specificare un numero di parametro in posizione più elevato rispetto al numero di parametri nell'istruzione SQL, il valore del parametro verrà ignorato quando viene eseguita l'istruzione.  
  
-   Il tipo di parametro (input, input/output o di output). Tranne che per i parametri nelle chiamate a procedure, tutti i parametri sono parametri di input. Per altre informazioni, vedere [parametri delle Procedure](../../../odbc/reference/develop-app/procedure-parameters.md), più avanti in questa sezione.  
  
-   La C lunghezza dei dati byte, l'indirizzo e tipo della variabile associato al parametro. Il driver deve essere in grado di convertire i dati dal tipo di dati C per il tipo di dati SQL o viene restituito un errore. Per un elenco delle conversioni supportate, vedere [conversione di dati da C a tipi di dati SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) nell'appendice d: Tipi di dati.  
  
-   Il tipo di dati SQL, precisione e scala del parametro stesso.  
  
-   L'indirizzo di un buffer di lunghezza/indicatore. Fornisce la lunghezza in byte di dati carattere o binario, specifica che i dati sono NULL o specifica che i dati verranno inviati con **SQLPutData**. Per altre informazioni, vedere [usando i valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Ad esempio, il codice seguente associa *SalesPerson* e *CustID* ai parametri per le colonne CustomerID e venditore. Poiché *SalesPerson* contiene dati di tipo carattere, che è di lunghezza variabile, il codice specifica la lunghezza in byte dei *SalesPerson* (11) e associa *SalesPersonLenOrInd* a contiene la lunghezza in byte dei dati in *venditore*. Queste informazioni non sono necessarie per *CustID* perché contiene dati integer, che è di lunghezza fissa.  
  
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
  
 Quando **SQLBindParameter** viene chiamato, il driver di queste informazioni vengono memorizzate nella struttura per l'istruzione. Quando viene eseguita l'istruzione, Usa le informazioni per recuperare i dati del parametro e inviarlo all'origine dati.  
  
> [!NOTE]  
>  In ODBC 1.0, sono stati associati parametri **SQLSetParam**. Gestione Driver viene eseguito il mapping tra le chiamate **SQLSetParam** e **SQLBindParameter**, a seconda le versioni di ODBC utilizzata dalle applicazioni e driver.
