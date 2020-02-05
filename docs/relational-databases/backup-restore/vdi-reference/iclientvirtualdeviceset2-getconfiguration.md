---
title: IClientVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IClientVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 5d7d42d081b0494feeb5c2b221575e0d5df1143a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847452"
---
# <a name="iclientvirtualdeviceset2getconfiguration-vdi"></a>IClientVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **GetConfiguration** viene usata per attendere che il server configuri il set di dispositivi virtuali.

## <a name="syntax"></a>Sintassi

```c
HRESULT IClientVirtualDeviceSet2::GetConfiguration (
   DWORD         dwTimeOut,
   VDConfig*      pCfg
);
```

## <a name="parameters"></a>Parametri

*DwTimeOut* Timeout in millisecondi. Usare INFINITE per impedire il timeout.

*pCfg* Dopo la corretta esecuzione, contiene la configurazione selezionata dal server. Per altre informazioni, vedere Configurazione.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | La configurazione è stata restituita. |
| VD_E_ABORT | SignalAbort è stato richiamato. |
| VD_E_TIMEOUT | Timeout della funzione. |

## <a name="remarks"></a>Osservazioni

Questa funzione causa un blocco in uno stato di avviso. Una volta completata la chiamata, è possibile aprire i dispositivi nel set di dispositivi virtuali.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).