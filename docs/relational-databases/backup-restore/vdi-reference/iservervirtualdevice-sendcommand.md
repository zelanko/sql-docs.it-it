---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDevice::SendCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: f03e87863d21abfc4abf91811616cbacd14caff2
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96125376"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La funzione **SendCommand** invia un comando al client usando un oggetto dispositivo virtuale restituito da IServerVirtualDeviceSet2::OpenDevice.

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDevice::SendCommand (
   VDS_Command*   pCmd
);
```

## <a name="parameters"></a>Parametri

*pCmd* Puntatore a un blocco di richiesta di comando. Per altre informazioni, vedere Comandi. Il campo completionFunction deve essere impostato in modo da puntare all'indirizzo di una funzione con la firma seguente:

```c
void callbackFunction ( VDS_Command *pCmd);
```

Questo callback viene eseguito dall'agente di completamento quando il client indica che è stato completato un comando. SQL Server imposta il campo completionContext di pCmd. Lo scopo è fornire il contesto alla funzione di callback.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Il comando viene accodato nel client. |
| VD_E_QUEUE_FULL | Coda del dispositivo piena. |
| VD_E_IO_ERROR | Il dispositivo è in uno stato IO-ERROR . |
| VD_E_PROTOCOL | Il dispositivo non è attivo. |

## <a name="remarks"></a>Osservazioni

Quando si verifica un errore durante il tentativo di invio del comando, viene richiamata la funzione di callback e il completionCode nel buffer dei comandi viene impostato come segue:

| completionCode | Errore |
|---|---|
| VD_E_QUEUE_FULL | ERROR_NO_SYSTEM_RESOURCES |
| VD_E_IO_ERROR   | ERROR_IO_DEVICE |
| VD_E_PROTOCOL   | ERROR_INVALID_HANDLE |
| VD_E_ABORT      | ERROR_OPERATION_ABORTED |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).