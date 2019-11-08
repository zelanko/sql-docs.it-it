---
title: SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLFetchScroll function
ms.assetid: 524a3985-a08d-4445-99e0-bb551a666615
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a9884121808df6a4546ed073eca128788acc95e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786822"
---
# <a name="sqlfetchscroll"></a>SQLFetchScroll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  **SQLFetchScroll** restituisce un set di righe di dati all'applicazione. Le dimensioni del set di righe vengono impostate utilizzando [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client supporta tutte le istruzioni di recupero definite, ad esempio SQL_FETCH_RELATIVE, con le limitazioni seguenti:  
  
-   Se per l'istruzione è definito un cursore forward-only, è necessario specificare SQL_FETCH_NEXT e qualsiasi tentativo di recupero effettuato con altre modalità comporterà la restituzione di un errore.  
  
-   SQL_FETCH_BOOKMARK è supportato solo per i cursori statici e gestiti da keyset.  
  
## <a name="sqlfetchscroll-support-for-enhanced-date-and-time-features"></a>Supporto di SQLFetchScroll per le caratteristiche avanzate di data e ora  
 I valori della colonna dei risultati dei tipi data/ora vengono convertiti come descritto in [conversioni da SQL a C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md).  
  
 Per ulteriori informazioni, vedere [miglioramenti &#40;di data e ora&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md).  
  
## <a name="sqlfetchscroll-support-for-large-clr-udts"></a>Supporto SQLFetchScroll per i tipi CLR definiti dall'utente di grandi dimensioni  
 **SQLFetchScroll** supporta i tipi CLR definiti dall'utente di grandi dimensioni. Per ulteriori informazioni, vedere [tipi &#40;CLR definiti dall'utente di grandi&#41;dimensioni ODBC](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md).  
  
## <a name="see-also"></a>Vedere anche  
   [funzione SQLFetchScroll](https://go.microsoft.com/fwlink/?LinkId=59343)  
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
