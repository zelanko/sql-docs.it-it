---
title: Recuperare informazioni sul set di risultati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f1c65841db0fdfd386891cfbd03bdee483ce25f6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300381"
---
# <a name="processing-results---retrieve-result-set-information"></a>Elaborazione dei risultati - Recuperare le informazioni sul set di risultati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

    
### <a name="to-get-information-about-a-result-set"></a>Per recuperare informazioni su un set di risultati  
  
1.  Chiamare [SQLNumResultCols](../../relational-databases/native-client-odbc-api/sqlnumresultcols.md) per ottenere il numero di colonne nel set di risultati.  
  
2.  Per ogni colonna del set di risultati, effettuare le operazioni seguenti:  
  
    -   Chiamare [SQLDescribeCol](../../relational-databases/native-client-odbc-api/sqldescribecol.md) per ottenere informazioni sulla colonna risultato.  
  
     Oppure  
  
    -   Chiamare [SQLColAttribute](../../relational-databases/native-client-odbc-api/sqlcolattribute.md) per ottenere informazioni specifiche sul descrittore sulla colonna risultato.  
  
## <a name="see-also"></a>Vedere anche  
[Elaborare i risultati &#40;&#41;ODBC](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinazione delle caratteristiche di un set di risultati &#40;ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
