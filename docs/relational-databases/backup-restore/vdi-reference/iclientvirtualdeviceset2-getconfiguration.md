---
title: IClientVirtualDeviceSet2::GetConfiguration
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IClientVirtualDeviceSet2::GetConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 5d46efb493dc67c38affc25f99871f3ff4617ecb
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125392"
---
# <a name="iclientvirtualdeviceset2getconfiguration-vdi"></a>IClientVirtualDeviceSet2::GetConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

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