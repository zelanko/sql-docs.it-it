---
title: SQLError (Driver ODBC di Visual FoxPro) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLError function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8315ec16-1c22-447a-a577-39bd94f61070
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0d1247217905187cfb2dbaca6d7b7b562d0175bd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298681"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (driver ODBC Visual FoxPro)
> [!NOTE]  
>  In questo argomento sono contenute informazioni specifiche del driver ODBC di Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: Completo  
  
 Conformità API ODBC: livello di baseODBC API Conformance: Core Level  
  
 Restituisce informazioni sull'errore o sullo stato relative all'ultimo errore. Il driver gestisce uno stack o un elenco di errori che possono essere restituiti per il *hstmt*, *hdbc*, e *henv* argomenti, a seconda di come viene effettuata la chiamata a **SQLError.** La coda degli errori viene scaricata dopo ogni istruzione.  
  
 Nella tabella seguente vengono descritti gli argomenti **SQLError** e i valori restituiti utilizzati dal driver.  
  
|Argomento SQLError|Descrizione del valore restituito|  
|-----------------------|------------------------------|  
|*szSQLState (informazioni in lingua inglese)*|Valore per SQLSTATE rappresentato dall'errore.|  
|*PfNativeError (errore pfNative)*|Un valore diverso da zero indica un messaggio di errore nativo del [driver ODBC di Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Il valore zero indica che l'errore è stato rilevato dal driver e mappato al codice di [errore ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)appropriato.|  
|*Szerrormsg*|Testo per l'errore nativo o l'errore ODBC.|  
|*pcbErrorMsg (informazioni in due)*|Lunghezza del testo del messaggio più la lunghezza degli identificatori.|  
  
 Per ulteriori informazioni sui messaggi di errore del driver, vedere [Cenni preliminari](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md)sui messaggi di errore . Per ulteriori informazioni su questa funzione, vedere [SQLError](../../odbc/reference/syntax/sqlerror-function.md) in *ODBC Programmer's Reference*.
