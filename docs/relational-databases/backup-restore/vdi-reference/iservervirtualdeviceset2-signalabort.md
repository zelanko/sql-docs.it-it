---
title: IServerVirtualDeviceSet2::SignalAbort
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDeviceSet2::SignalAbort.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b61a972d7b379ff40440124c875d8d49a7af1835
ms.sourcegitcommit: dc8697bdd950babf419b4f1e93b26bb789d39f4a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2019
ms.locfileid: "70847172"
---
# <a name="iservervirtualdeviceset2signalabort-vdi"></a>IServerVirtualDeviceSet2::SignalAbort (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **SignalAbort** segnala che dovrebbe verificarsi una terminazione anomala.

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDeviceSet2::SignalAbort ();
```

## <a name="return-value"></a>Valore restituito

Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore NOERROR indica l'esito positivo della chiamata del metodo. Un valore diverso da zero indica che si è verificato un errore.

## <a name="remarks"></a>Remarks

In qualsiasi momento il server può scegliere di interrompere l'operazione di backup o ripristino.

Questa routine segnala che tutte le operazioni devono essere interrotte. L'interfaccia nel suo complesso entra in uno stato di interruzione. Nessun altro comando viene accettato in alcun dispositivo. L'agente di completamento restituisce ERROR_OPERATION_ABORTED per ogni richiesta in sospeso e torna al chiamante. Tutti i completamenti registrati nel client vengono ignorati.

Il server garantisce che non vi siano altri usi richiesti per i buffer o i dispositivi restituiti dall'interfaccia dispositivo virtuale. Il server esegue quindi una pulizia delle terminazioni anomale, che deve includere la chiamata della funzione IServerVirtualDeviceSet2::Close.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).