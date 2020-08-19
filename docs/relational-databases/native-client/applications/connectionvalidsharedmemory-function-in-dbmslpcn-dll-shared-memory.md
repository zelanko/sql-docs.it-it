---
description: Funzione ConnectionValidSharedMemory nella memoria condivisa dbmslpcn.dll
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
ms.openlocfilehash: 02247866c1f83693202d649d1c05be31214b5ded
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498934"
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
  
  
