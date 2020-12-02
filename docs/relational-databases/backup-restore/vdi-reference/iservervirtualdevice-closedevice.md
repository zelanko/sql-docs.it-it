---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDevice::CloseDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 61d877fddb32f6455303a006e8955b1042ce7aa6
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128904"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La funzione **CloseDevice** chiude un dispositivo virtuale che è stato aperto con IServerVirtualDeviceSet2::OpenDevice

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDevice::CloseDevice ();
```

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| VD_E_CLOSE | Il dispositivo è già chiuso. |
| VD_E_ABORT | L'interfaccia è nello stato di interruzione. |

## <a name="remarks"></a>Osservazioni

CloseDevice non è necessario dopo l'uso di SignalAbort per forzare la terminazione anomala. Se CloseDevice viene richiamato dopo l'uso di SignalAbort, non viene eseguita alcuna azione.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).