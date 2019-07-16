---
title: Funzione ConnectionValidSharedMemory nella memoria condivisa dbmslpcn | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49885ca7d11ef7dbbe716375c399fe5fc4d4c93e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069309"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Funzione ConnectionValidSharedMemory nella memoria condivisa dbmslpcn.dll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  La funzione determina se la memoria condivisa di SQL Server è installato e attivato.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parametri  
 *szServerName*  
  
-   Tipo: **char\***  
  
-   Il nome del server SQL.  
  
## <a name="return-value"></a>Valore restituito  
 Digitare:  **BOOL**  
  
 Restituisce 0 se non è valido. Else restituisce diverso da zero.  
  
  
