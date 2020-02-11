---
title: Liberazione di un handle di istruzione | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9b1a155f7d2ee6cc5f92d46c2bb744168dc5ebc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63200053"
---
# <a name="freeing-a-statement-handle"></a>Rilascio di un handle di istruzione
  È più efficiente riutilizzare handle di istruzione anziché eliminarli e allocarne di nuovi. Prima di eseguire una nuova istruzione SQL su un handle di istruzione, le applicazioni devono verificare che le impostazioni delle istruzioni correnti siano corrette. Tra le impostazioni sono inclusi gli attributi di istruzione, le associazioni di parametri e le associazioni dei set di risultati. In genere, i parametri e i set di risultati per l'istruzione SQL precedente devono essere non associati chiamando [SQLFreeStmt](../native-client-odbc-api/sqlfreestmt.md) con le opzioni SQL_RESET_PARAMS e SQL_UNBIND e quindi riassociati per la nuova istruzione SQL.  
  
 Al termine dell'utilizzo dell'istruzione, l'applicazione chiama [SQLFreeHandle](../native-client-odbc-api/sqlfreehandle.md) per liberare l'istruzione. Si noti che **Disconnect** libera automaticamente tutte le istruzioni in una connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Esecuzione di query &#40;ODBC&#41;](executing-queries-odbc.md)  
  
  
