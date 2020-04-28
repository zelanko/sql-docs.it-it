---
title: SQLError (driver ODBC Visual FoxPro) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298681"
---
# <a name="sqlerror-visual-foxpro-odbc-driver"></a>SQLError (driver ODBC Visual FoxPro)
> [!NOTE]  
>  Questo argomento contiene informazioni specifiche del driver ODBC Visual FoxPro. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Supporto: completo  
  
 Conformità API ODBC: livello principale  
  
 Restituisce informazioni sull'errore o sullo stato dell'ultimo errore. Il driver gestisce uno stack o un elenco di errori che possono essere restituiti per gli argomenti *HSTMT*, *HDBC*e *HENV* , a seconda del modo in cui viene effettuata la chiamata a **SQLError** . La coda degli errori viene scaricata dopo ogni istruzione.  
  
 Nella tabella seguente vengono descritti gli argomenti e i valori restituiti di **SQLError** utilizzati dal driver.  
  
|Argomento SQLError|Descrizione valore restituito|  
|-----------------------|------------------------------|  
|*szSQLState*|Valore per il valore SQLSTATE rappresentato dall'errore.|  
|*pfNativeError*|Un valore diverso da zero indica un [messaggio di errore nativo del driver ODBC Visual FoxPro](../../odbc/microsoft/visual-foxpro-odbc-driver-native-error-messages.md). Un valore pari a zero indica che l'errore è stato rilevato dal driver ed è stato eseguito il mapping al [codice di errore ODBC](../../odbc/microsoft/odbc-error-codes-visual-foxpro-odbc-driver.md)appropriato.|  
|*szErrorMsg*|Testo per l'errore nativo o ODBC.|  
|*pcbErrorMsg*|Lunghezza del testo del messaggio più la lunghezza degli identificatori.|  
  
 Per ulteriori informazioni sui messaggi di errore del driver, vedere [Cenni preliminari sui messaggi di errore](../../odbc/microsoft/error-messages-visual-foxpro-odbc-driver.md). Per ulteriori informazioni su questa funzione, vedere [SQLError](../../odbc/reference/syntax/sqlerror-function.md) in *ODBC Programmer ' s Reference*.
