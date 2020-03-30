---
title: IServerVirtualDeviceSet2::Open
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDeviceSet2::Open.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 552394db26a1b236a4d6997f6dbfba77d12086ee
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "70847222"
---
# <a name="iservervirtualdeviceset2open-vdi"></a>IServerVirtualDeviceSet2::Open (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **Open** apre il set di dispositivi virtuali nel server e deve essere la prima chiamata eseguita usando l'handle di interfaccia fornito da COM.

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDeviceSet2::Open (
   LPCWSTR      lpInstanceName,
   LPCWSTR      lpName
);
```

## <a name="parameters"></a>Parametri

*lpInstanceName* Questa stringa identifica l'istanza di SQL Server a cui verrà inviato il comando SQL. È possibile passare NULL per identificare l'istanza predefinita nel computer corrente.

*lpName* Fornito dalla prima clausola VIRTUAL_DEVICE= del comando BACKUP o RESTORE. Questo nome viene usato come chiave per ottenere l'accesso al set di dispositivi virtuali creato dal client.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Funzione completata. |
| VD_E_INVALID | Il nome fornito non ha identificato un set di dispositivi virtuali accessibile per il server. |

## <a name="remarks"></a>Osservazioni

Dopo che questa funzione è stata richiamata correttamente, il server può procedere alla configurazione del set di dispositivi virtuali tramite GetConfiguration e SetConfiguration.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).