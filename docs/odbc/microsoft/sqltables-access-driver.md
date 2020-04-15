---
title: SQLTables (Driver di accesso) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLTables function [ODBC], Access Driver
- Access driver [ODBC], SQLTables
ms.assetid: 94423cf9-341a-4db6-bb10-8f5448df7fc3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: df3a23af365efbef6a0f0da2c52568501425ecb3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306092"
---
# <a name="sqltables-access-driver"></a>SQLTables (driver Access)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver di accesso. Per informazioni generali su questa funzione, vedere l'argomento appropriato in [Riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|Argomento|Commenti|  
|--------------|--------------|  
|*szTableOwner*|L'unico argomento valido per *szTableOwner* è NULL perché nessuno dei driver supporta i nomi dei proprietari. Con *szTableOwner* impostato su NULL, vengono restituite tutte le tabelle. NULL viene restituito nella colonna TABLE_OWNER.|  
|*SzTableQualifier (qualificatore di szTable)*|Nella colonna TABLE_QUALIFIER **SQLTables** restituirà il percorso di un file di database.|  
|*SzTableType (Tipo di SzTableType)*|Quando viene utilizzato il driver di Microsoft Access, "SYSTEM TABLE" è supportato per *szTableType* per le tabelle di sistema, "SYNONYM" è supportato per le tabelle associate e "VIEW" è supportato per le query di restituzione delle righe.|  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione SQLTables](../../odbc/reference/syntax/sqltables-function.md)
