---
title: IServerVirtualDevice::CloseDevice
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDevice::CloseDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c73649e2a4301e94f8e68504222cc0122061f25f
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847432"
---
# <a name="iservervirtualdeviceclosedevice-vdi"></a>IServerVirtualDevice::CloseDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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