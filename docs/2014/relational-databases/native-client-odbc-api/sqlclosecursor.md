---
title: SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLCloseCursor function
ms.assetid: e7134d65-5c1c-4ae2-b119-d9b4b9a42483
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da7d6541f7bf31920519cc7462bdfd24a5f6dc0d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63067687"
---
# <a name="sqlclosecursor"></a>SQLCloseCursor
  **SQLCloseCursor** sostituisce [SQLFreeStmt](sqlfreestmt.md) con un *opzione* valore SQL_CLOSE. Alla ricezione di **SQLCloseCursor**, il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client elimina le righe del set di risultati in sospeso. Notare che le associazioni di parametro e colonna dell'istruzione, se presenti, non vengono modificate da **SQLCloseCursor**.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLCloseCursor](https://go.microsoft.com/fwlink/?LinkId=59331)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
