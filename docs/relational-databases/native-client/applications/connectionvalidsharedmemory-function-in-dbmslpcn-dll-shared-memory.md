---
title: dbmslpcn.dll ConnectionValidSharedMemory
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b8fea72023f929fb01c8ee5ca699a1d695aa0788
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005742"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Funzione ConnectionValidSharedMemory nella memoria condivisa dbmslpcn.dll
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La funzione determina se SQL Server la memoria condivisa è installata e attiva.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parametri  
 *szServerName*  
  
-   Tipo: **char \* **  
  
-   Nome del server SQL.  
  
## <a name="return-value"></a>Valore restituito  
 Tipo: **bool**  
  
 Restituisce 0 se non è valido; else restituisce un valore diverso da zero.  
  
  
