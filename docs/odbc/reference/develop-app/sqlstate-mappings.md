---
title: Mapping SQLSTATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3987085d7d04bf248bcc728c3bcd1ee5503d9af1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107357"
---
# <a name="sqlstate-mappings"></a>Mapping di SQLSTATE
In questo argomento vengono illustrati i valori SQLSTATE per ODBC *2. x* e ODBC *3. x*. Per ulteriori informazioni sui valori SQLSTATE ODBC *3. x* , vedere [Appendice A: codici di errore ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 In ODBC *3. x*, vengono restituiti HYxxx sqlstates anziché S1xxx e vengono restituiti 42Sxx sqlstates anziché S00XX. Questa operazione è stata eseguita per l'allineamento con gli standard Open Group e ISO. In molti casi, il mapping non è uno-a-uno perché gli standard hanno ridefinito l'interpretazione di diversi SQLSTATE.  
  
 Quando un'applicazione ODBC *2. x* viene aggiornata a un'applicazione ODBC *3. x* , è necessario modificare l'applicazione in modo da prevedere sqlstates ODBC *3. x* anziché ODBC *2. x* sqlstates. Nella tabella seguente sono elencati i SQLState ODBC *3. x* a cui è stato eseguito il mapping di ogni SQLState ODBC *2. x* .  
  
 Quando l'attributo SQL_ATTR_ODBC_VERSION Environment è impostato su SQL_OV_ODBC2, il driver invia sqlstates ODBC *2. x* invece di ODBC *3. x* sqlstates quando viene chiamato **SQLGetDiagField** o **SQLGetDiagRec** . Per determinare un mapping specifico, è possibile notare il valore SQLSTATE ODBC *2. x* nella colonna 1 della tabella seguente che corrisponde al valore SQLSTATE ODBC *3. x* nella colonna 2.  
  
|ODBC *2. x* SQLSTATE|ODBC *3. x* SQLSTATE|Commenti|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC *2. x* SQLSTATE S1002 è mappato a *ODBC 3. x* SQLSTATE 07009 se la funzione sottostante è **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch**, **SQLFetchScroll**o **SQLGetData**.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Restituito per un utilizzo non valido di un puntatore null.|  
|S1009|HY024|Restituito per un valore di attributo non valido.|  
|S1009|HY092|Restituito per l'aggiornamento o l'eliminazione di dati tramite una chiamata a **SQLSetPos**o per l'aggiunta, l'aggiornamento o l'eliminazione di dati tramite una chiamata a **SQLBulkOperations**, quando la concorrenza è di sola lettura.|  
|S1010|HY010 HY007|Viene eseguito il mapping di SQLSTATE S1010 a SQLSTATE HY007 quando **SQLDescribeCol** viene chiamato prima di chiamare **SQLPrepare**, **SQLExecDirect**o una funzione di catalogo per *statementHandle*. In caso contrario, viene eseguito il mapping di SQLSTATE S1010 a SQLSTATE HY010.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3. x* SQLSTATE 07009 è mappato a ODBC *2. x* SQLSTATE S1093 se la funzione sottostante è **SQLBindParameter** o **SQLDescribeParam**.|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC *3. x* SQLSTATE 07008 è mappato a ODBC *2. x* SQLSTATE S1000.
