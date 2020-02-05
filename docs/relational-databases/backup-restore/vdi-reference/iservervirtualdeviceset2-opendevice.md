---
title: IServerVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDeviceSet2::OpenDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: af24aff4bbb8f0eefa14363453e962c0a90d610e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847212"
---
# <a name="iservervirtualdeviceset2opendevice-vdi"></a>IServerVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **OpenDevice** ottiene le interfacce dispositivo virtuale dal set di dispositivi virtuali.

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDeviceSet2::OpenDevice (
   LPCWSTR                     lpName,
   IServerVirtualDevice**      ppVirtualDevice
);
```

## <a name="parameters"></a>Parametri

*lpName* Fornito dalla prima clausola VIRTUAL_DEVICE= del comando BACKUP o RESTORE. Questo nome viene usato come chiave per ottenere l'accesso al set di dispositivi virtuali creato dal client.

*ppVirtualDevice* Usato per restituire un'interfaccia dispositivo virtuale.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Funzione completata. |
| VD_E_OPEN |Tutti i dispositivi sono stati aperti. |

## <a name="remarks"></a>Osservazioni

Ogni chiamata restituisce il successivo dispositivo non aperto. La funzione può essere chiamata solo per il numero di volte uguale al numero di dispositivi specificato nella configurazione del set di dispositivi virtuali.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).