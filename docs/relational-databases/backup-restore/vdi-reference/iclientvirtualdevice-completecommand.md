---
title: IClientVirtualDevice::CompleteCommand
titlesuffix: SQL Server VDI reference
description: Questo articolo include informazioni di riferimento sul comando IClientVirtualDevice::CompleteCommand.
ms.date: 08/30/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.technology: backup-restore
ms.topic: reference
author: cawrites
ms.author: chadam
ms.openlocfilehash: 367d398160daa8b9a9da5bfc3a3285cf61b6d085
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/23/2020
ms.locfileid: "96128989"
---
# <a name="iclientvirtualdevicecompletecommand-vdi"></a>IClientVirtualDevice::CompleteCommand (VDI)

[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]

La funzione **CompleteCommand** viene usata per notificare a SQL Server il completamento di un comando. Devono essere restituite le informazioni di completamento appropriate per il comando.

## <a name="syntax"></a>Sintassi

```c
HRESULT IClientVirtualDevice::CompleteCommand (
   VDC_Command*         const pCmd,
   UINT32               dwCompletionCode,
   UINT32               dwBytesTransferred,
   UINT64               dwlPosition
);
```

## <a name="parameters"></a>Parametri

*pCmd* Indirizzo di un comando restituito in precedenza da IClientVirtualDevice::GetCommand.

*dwCompletionCode* Codice di stato WIN32 che indica lo stato di completamento. Questo parametro deve essere restituito per tutti i comandi. Il codice restituito deve essere appropriato per il comando in esecuzione. ERROR_SUCCESS viene usato in tutti i casi per indicare un comando eseguito correttamente. Per l'elenco completo dei codici possibili, vedere il file Winerror.h. Un elenco dei codici di stato tipici per ogni comando è disponibile in Comandi.

*dwBytesTransferred* Numero di byte trasferiti correttamente. Viene restituito solo per i comandi di trasferimento dati Read e Write.

*dwlPosition* Risposta al solo comando GetPosition.

## <a name="return-value"></a>Valore restituito

|Valore restituito | Spiegazione |
|---|---|
| NOERROR | Il completamento è stato annotato correttamente. |
| VD_E_INVALID | pCmd non è un comando attivo. |
| VD_E_ABORT | Interruzione segnalata. |
| VD_E_PROTOCOL | Il dispositivo non è aperto. |

## <a name="next-steps"></a>Passaggi successivi

Per altre informazioni, vedere [Informazioni di riferimento sull'interfaccia dispositivo virtuale di SQL Server](reference-virtual-device-interface.md).
