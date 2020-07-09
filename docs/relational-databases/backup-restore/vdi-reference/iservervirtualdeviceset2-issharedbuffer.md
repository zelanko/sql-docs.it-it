---
title: IServerVirtualDeviceSet2::IsSharedBuffer
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDeviceSet2::IsSharedBuffer.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 3c0161639e2fb11bc3f1525ea3ffad32843a183d
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898958"
---
# <a name="iservervirtualdeviceset2issharedbuffer-vdi"></a>IServerVirtualDeviceSet2::IsSharedBuffer (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La funzione **IsSharedBuffer** determina se l'indirizzo del buffer specificato fa riferimento a uno dei buffer condivisi resi disponibili dal metodo AllocateBuffer.

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDeviceSet2::IsSharedBuffer (
   LPVOID   lpBuffer
);
```

## <a name="parameters"></a>Parametri

*lpBuffer* Indirizzo di un buffer.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| TRUE | Il buffer è un buffer condiviso. |
| FALSE | Il buffer non fa parte del set di dispositivi virtuali. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).