---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IClientVirtualDeviceSet2::MapBufferHandle.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 23bb125d8744cf51f6b72187b6a251e27fb84f05
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896891"
---
# <a name="iclientvirtualdeviceset2mapbufferhandle-vdi"></a>IClientVirtualDeviceSet2::MapBufferHandle (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La funzione **MapBufferHandle** viene usata per ottenere un indirizzo del buffer valido da un handle del buffer ottenuto da un altro processo.

## <a name="syntax"></a>Sintassi

```c
HRESULT IClientVirtualDeviceSet2::MapBufferHandle (
   DWORD      dwBuffer,
   BYTE**      ppBuffer
);
```

## <a name="parameters"></a>Parametri

*dwBuffer* Handle restituito da IClientVirtualDeviceSet2::GetBufferHandle.

*ppBuffer* Indirizzo del buffer valido nel processo corrente.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Funzione completata. |
| VD_E_PROTOCOL | Il set di dispositivi virtuali non è attualmente aperto. |
| VD_E_INVALID | ppBuffer è un handle non valido. |

## <a name="remarks"></a>Osservazioni

Prestare attenzione a comunicare correttamente gli handle. Gli handle sono locali in un singolo set di dispositivi virtuali. I processi partner che condividono un handle devono assicurarsi che gli handle del buffer vengano usati solo nell'ambito del set di dispositivi virtuali da cui è stato originariamente ottenuto il buffer.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).