---
title: IServerVirtualDevice::SendCommand
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDevice::SendCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: c75cd206557547f55d47eec0a7aec52cc0069b71
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847512"
---
# <a name="iservervirtualdevicesendcommand-vdi"></a>IServerVirtualDevice::SendCommand (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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