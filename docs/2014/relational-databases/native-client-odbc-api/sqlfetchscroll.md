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
author: rothja
ms.author: jroth
ms.openlocfilehash: eecf9714a97577ff490b642cee5b9c380333e40b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85022506"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
  **SQLFetchScroll** restituisce un set di righe di dati all'applicazione. Le dimensioni del set di righe vengono impostate utilizzando [SQLSetStmtAttr](sqlsetstmtattr.md). Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta tutte le istruzioni di recupero definite, ad esempio SQL_FETCH_RELATIVE, con le limitazioni seguenti:  
  
-   Se per l'istruzione è definito un cursore forward-only, è necessario specificare SQL_FETCH_NEXT e qualsiasi tentativo di recupero effettuato con altre modalità comporterà la restituzione di un errore.  
  
-   SQL_FETCH_BOOKMARK è supportato solo per i cursori statici e gestiti da keyset.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>Supporto di SQLFetchScroll per le caratteristiche avanzate di data e ora  
 I valori della colonna dei risultati dei tipi data/ora vengono convertiti come descritto in [conversioni da SQL a C](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Per ulteriori informazioni, vedere [miglioramenti di data e ora &#40;&#41;ODBC ](../native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>Supporto SQLFetchScroll per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLFetchScroll** supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi CLR definiti dall'utente di grandi dimensioni &#40;&#41;ODBC ](../native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFetchScroll (funzione)](https://go.microsoft.com/fwlink/?LinkId=59343)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
