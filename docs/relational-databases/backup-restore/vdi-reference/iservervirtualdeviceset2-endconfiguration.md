---
title: IServerVirtualDeviceSet2::EndConfiguration
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IServerVirtualDeviceSet2::EndConfiguration.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d2ed7365e9a0e895a7deb0ba20d57868a947b350
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/02/2020
ms.locfileid: "85896337"
---
# <a name="iservervirtualdeviceset2endconfiguration-vdi"></a>IServerVirtualDeviceSet2::EndConfiguration (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La funzione **EndConfiguration** comunica all'interfaccia VDI che il server ha completato la configurazione.

## <a name="syntax"></a>Sintassi

```c
HRESULT IServerVirtualDeviceSet2::EndConfiguration ();
```

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Funzione completata. |
| VD_E_ABORT | È stata richiesta l'interruzione. |
| VD_E_PROTOCOL | Il set non è nello stato configurabile. |
| VD_E_MEMORY | Non è stato possibile ottenere la memoria richiesta tramite le chiamate ' RequestBuffers'. Il set rimane nello stato configurabile senza spazio del buffer disponibile. Il server può ridurre i requisiti del buffer o interrompere l'operazione. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).