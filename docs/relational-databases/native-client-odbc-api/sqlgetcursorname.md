---
title: SQLGetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetCursorName function
ms.assetid: 3a427a23-28ef-49aa-b9ec-6cab0914bdf3
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 81fcdac796dcaf185ee2929c5d981a1f88edb26d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73786555"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Se l'applicazione non specifica un nome di cursore, il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native client ne genera uno per l'applicazione durante la generazione del cursore. L'applicazione può utilizzare **SQLGetCursorName** per recuperare il nome del cursore definito dal driver per le istruzioni Update e Delete posizionate. Non è necessario che l'applicazione chiami **SQLSetCursorName** per sfruttare le istruzioni di manipolazione dei dati posizionate.  
  
## <a name="see-also"></a>Vedere anche  
   [funzione SQLGetCursorName](https://go.microsoft.com/fwlink/?LinkId=59349)  
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
