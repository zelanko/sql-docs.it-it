---
title: SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3c9614a71c0015d17178a57d33c5fd0d9b62433c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53358853"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll** restituisce un set di righe di dati all'applicazione. La dimensione del set di righe viene impostata tramite [SQLSetStmtAttr](sqlsetstmtattr.md). Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client supporta tutte le istruzioni fetch definito (ad esempio SQL_FETCH_RELATIVE) con le limitazioni seguenti:  
  
-   Se per l'istruzione è definito un cursore forward-only, è necessario specificare SQL_FETCH_NEXT e qualsiasi tentativo di recupero effettuato con altre modalità comporterà la restituzione di un errore.  
  
-   SQL_FETCH_BOOKMARK è supportato solo per i cursori statici e gestiti da keyset.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>Supporto di SQLFetchScroll per le caratteristiche avanzate di data e ora  
 I valori di colonna risultato dei tipi data/ora vengono convertiti come descritto in [le conversioni da SQL a C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Per altre informazioni, vedere [data e miglioramenti per la fase &#40;ODBC&#41;](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>Supporto SQLFetchScroll per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLFetchScroll** supporta grandi CLR tipi definiti dall'utente (UDT). Per altre informazioni, vedere [Large CLR User-Defined tipi &#40;ODBC&#41;](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLFetchScroll](https://go.microsoft.com/fwlink/?LinkId=59343)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
