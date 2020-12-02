---
title: IClientVirtualDeviceSet2::MapBufferHandle
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IClientVirtualDeviceSet2::MapBufferHandle.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 70f6d117fd7a0349f2da2e03ff2603eaf55898fe
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128964"
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