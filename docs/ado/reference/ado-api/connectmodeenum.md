---
description: ConnectModeEnum
title: ConnectModeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ConnectModeEnum
helpviewer_keywords:
- ConnectModeEnum enumeration [ADO]
ms.assetid: 3792c294-5161-4538-a908-22a5fc50b85f
author: rothja
ms.author: jroth
ms.openlocfilehash: 10bc68683f337f5a0bdf6fc5679c4276925a4234
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88775850"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Specifica le autorizzazioni disponibili per la modifica dei dati in una [connessione](./connection-object-ado.md), l'apertura di un [record](./record-object-ado.md)o la specifica di valori per la proprietà [mode](./mode-property-ado.md) degli oggetti **record** e [flusso](./stream-object-ado.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica le autorizzazioni di sola lettura.|  
|**adModeReadWrite**|3|Indica le autorizzazioni di lettura/scrittura.|  
|**adModeRecursive**|0x400000|Utilizzato insieme agli altri valori * \* ShareDeny \* * (**adModeShareDenyNone**, **adModeShareDenyWrite**o **adModeShareDenyRead**) per propagare le restrizioni di condivisione a tutti i sottorecord del **record**corrente. Non ha alcun effetto se il **record** non contiene elementi figlio. Viene generato un errore di run-time se usato solo con **adModeShareDenyNone** . Tuttavia, può essere usato con **adModeShareDenyNone** se combinato con altri valori. Ad esempio, è possibile usare "**adModeRead** o **adModeShareDenyNone** o **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Consente ad altri utenti di aprire una connessione con qualsiasi autorizzazione. Impossibile negare l'accesso in lettura e in scrittura ad altri.|  
|**adModeShareDenyRead**|4|Impedisce ad altri utenti di aprire una connessione con autorizzazioni di lettura.|  
|**adModeShareDenyWrite**|8|Impedisce ad altri utenti di aprire una connessione con autorizzazioni di scrittura.|  
|**adModeShareExclusive**|12|Impedisce ad altri utenti di aprire una connessione.|  
|**adModeUnknown**|0|Valore predefinito. Indica che le autorizzazioni non sono state ancora impostate o non possono essere determinate.|  
|**adModeWrite**|2|Indica le autorizzazioni di sola scrittura.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums. ConnectMode. READ|  
|AdoEnums. ConnectMode. READWRITE|  
|(Non esiste alcun equivalente di AdoEnums. ConnectMode. ricorsivo)|  
|AdoEnums. ConnectMode. SHAREDENYNONE|  
|AdoEnums. ConnectMode. SHAREDENYREAD|  
|AdoEnums. ConnectMode. SHAREDENYWRITE|  
|AdoEnums. ConnectMode. SHAREEXCLUSIVE|  
|AdoEnums. ConnectMode. UNKNOWN|  
|AdoEnums. ConnectMode. WRITE|  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Proprietà Mode (ADO)](./mode-property-ado.md)  
        [Metodo Open (Record - ADO)](./open-method-ado-record.md)  
    :::column-end:::
    :::column:::
        [Metodo Open (Stream - ADO)](./open-method-ado-stream.md)  
        [Oggetto Stream (ADO)](./stream-object-ado.md)  
    :::column-end:::
:::row-end:::