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
ms.openlocfilehash: a0082245875f2f4dbf749876ede17dd0dc954737
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67910828"
---
# <a name="sqlgetcursorname"></a>SQLGetCursorName
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Se l'applicazione non specifica un nome di cursore, la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client ne genera uno al momento della generazione del cursore. L'applicazione può utilizzare **SQLGetCursorName** per recuperare il nome del cursore definito dal driver per le istruzioni UPDATE e DELETE posizionata. L'applicazione non è necessario chiamare **SQLSetCursorName** possa sfruttare i vantaggi di posizionato istruzioni di manipolazione dei dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLGetCursorName](https://go.microsoft.com/fwlink/?LinkId=59349)   
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
