---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: debf6f9dc4ac1326caf9fbf32b65f15f34a19094
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67933451"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Specifica le autorizzazioni disponibili per la modifica dei dati in una [connessione](../../../ado/reference/ado-api/connection-object-ado.md), l'apertura di un [record](../../../ado/reference/ado-api/record-object-ado.md)o la specifica di valori per la proprietà [mode](../../../ado/reference/ado-api/mode-property-ado.md) degli oggetti **record** e [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica le autorizzazioni di sola lettura.|  
|**adModeReadWrite**|3|Indica le autorizzazioni di lettura/scrittura.|  
|**adModeRecursive**|0x400000|Utilizzato insieme agli altri * \*\* valori ShareDeny* (**adModeShareDenyNone**, **adModeShareDenyWrite**o **adModeShareDenyRead**) per propagare le restrizioni di condivisione a tutti i sottorecord del **record**corrente. Non ha alcun effetto se il **record** non contiene elementi figlio. Viene generato un errore di run-time se usato solo con **adModeShareDenyNone** . Tuttavia, può essere usato con **adModeShareDenyNone** se combinato con altri valori. Ad esempio, è possibile usare "**adModeRead** o **adModeShareDenyNone** o **adModeRecursive**".|  
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
  
|||  
|-|-|  
|[Proprietà Mode (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Metodo Open (record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
