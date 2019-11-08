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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f2d998dd8b4444298ff67abc8369993d17e26f55
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73780332"
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
[ODBC risultati &#40;processo&#41;](../../relational-databases/native-client-odbc-how-to/processing-results-process-results.md)

[Determinazione delle caratteristiche di un set &#40;di risultati ODBC&#41;](../../relational-databases/native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
