---
title: Concorrenza del cursore (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3101da05e25cf67fda816bd889393bbebe8be3ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62711456"
---
# <a name="cursor-concurrency-odbc"></a>Concorrenza dei cursori (ODBC)
  Le operazioni dei cursori, come i tipi di cursore, sono influenzate dalle opzioni di concorrenza impostate dall'applicazione. Le opzioni di concorrenza vengono impostate utilizzando l'opzione SQL_ATTR_CONCURRENCY di [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). I tipi di concorrenza sono i seguenti:  
  
-   Di sola lettura (SQL_CONCUR_READONLY)  
  
-   Valori (SQL_CONCUR_VALUES)  
  
-   Versione di riga (SQL_CONCUR_ROWVER)  
  
-   Blocco (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà del cursore](cursor-properties.md)  
  
  
