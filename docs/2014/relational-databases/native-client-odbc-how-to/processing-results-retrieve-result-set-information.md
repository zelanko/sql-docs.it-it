---
title: Recuperare informazioni sul Set di risultati (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- result sets [ODBC]
- result sets [ODBC], fetching
ms.assetid: 34f235e4-f80b-4123-8764-9deb18506f14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a39a6715a9ba8ab08d846aabb96e5b0665a2aa43
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200298"
---
# <a name="retrieve-result-set-information-odbc"></a>Recuperare informazioni sul set di risultati (ODBC)
    
### <a name="to-get-information-about-a-result-set"></a>Per recuperare informazioni su un set di risultati  
  
1.  Chiamare [SQLNumResultCols](../native-client-odbc-api/sqlnumresultcols.md) per ottenere il numero di colonne nel set di risultati.  
  
2.  Per ogni colonna del set di risultati, effettuare le operazioni seguenti:  
  
    -   Chiamare [SQLDescribeCol](../native-client-odbc-api/sqldescribecol.md) per ottenere informazioni sulla colonna dei risultati.  
  
     Oppure  
  
    -   Chiamare [SQLColAttribute](../native-client-odbc-api/sqlcolattribute.md) per ottenere informazioni del descrittore specifiche sulla colonna dei risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per i risultati di elaborazione &#40;ODBC&#41;](../../database-engine/dev-guide/processing-results-how-to-topics-odbc.md)   
 [Determinazione delle caratteristiche di un Set di risultati &#40;ODBC&#41;](../native-client-odbc-results/determining-the-characteristics-of-a-result-set-odbc.md)  
  
  
