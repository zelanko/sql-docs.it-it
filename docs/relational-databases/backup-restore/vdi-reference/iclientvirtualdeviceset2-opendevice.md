---
title: IClientVirtualDeviceSet2::OpenDevice
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IClientVirtualDeviceSet2::OpenDevice.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: aff46d7240cf504b02e75d91b75d0ba746a24752
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "70847572"
---
# <a name="iclientvirtualdeviceset2opendevice-vdi"></a>IClientVirtualDeviceSet2::OpenDevice (VDI)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

La funzione **OpenDevice** apre uno dei dispositivi nel set di dispositivi virtuali.

## <a name="syntax"></a>Sintassi

```c
HRESULT IClientVirtualDeviceSet2::OpenDevice (
   LPCWSTR                  lpName,
   IClientVirtualDevice**   ppVirtualDevice

);
```

## <a name="parameters"></a>Parametri

*lpName* Identifica il dispositivo virtuale.

*ppVirtualDevice* Quando la funzione ha esito positivo, viene restituito un puntatore di interfaccia al dispositivo virtuale. Questa interfaccia viene usata per GetCommand e CompleteCommand.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Funzione completata. |
| VD_E_ABORT | È stata richiesta l'interruzione. |
| VD_E_OPEN |Tutti i dispositivi sono aperti. |
| VD_E_PROTOCOL | Il set non è nello stato di inizializzazione o questo particolare dispositivo è già aperto. |
| VD_E_INVALID | Il nome del dispositivo non è valido. Non è uno dei nomi noti inclusi nel set. |

## <a name="remarks"></a>Osservazioni

VD_E_OPEN può essere restituito senza problemi. Il client può chiamare OpenDevice per mezzo di un ciclo finché questo codice non viene restituito.
Se sono configurati più dispositivi, ad esempio n dispositivi, il set di dispositivi virtuali restituirà n interfacce di dispositivo univoche. Il primo dispositivo ha lo stesso nome del set di dispositivi virtuali. Gli altri dispositivi vengono denominati come specificato con le clausole VIRTUAL_DEVICE dell'istruzione BACKUP/RESTORE.

La funzione GetConfiguration può essere usata per attendere che i dispositivi possano essere aperti.

Se la funzione non riesce, viene restituito un valore Null tramite ppVirtualDevice.

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).