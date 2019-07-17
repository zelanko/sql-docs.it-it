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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67933451"
---
# <a name="connectmodeenum"></a>ConnectModeEnum
Specifica le autorizzazioni disponibili per la modifica dei dati in un [Connection](../../../ado/reference/ado-api/connection-object-ado.md), aprire un [Record](../../../ado/reference/ado-api/record-object-ado.md), o specificando i valori per il [modalità](../../../ado/reference/ado-api/mode-property-ado.md) proprietà del  **Record** e [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetti.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adModeRead**|1|Indica le autorizzazioni di sola lettura.|  
|**adModeReadWrite**|3|Indica le autorizzazioni di lettura/scrittura.|  
|**adModeRecursive**|0x400000|Usato in combinazione con l'altra *\*ShareDeny\** valori (**adModeShareDenyNone**, **adModeShareDenyWrite**, o **adModeShareDenyRead**) per propagare le restrizioni della condivisione dell'istanza corrente a tutti i **Record**. Non produce alcun effetto se il **Record** non ha elementi figlio. Viene generato un errore di run-time se viene usato con **adModeShareDenyNone** solo. Tuttavia, può essere utilizzato con **adModeShareDenyNone** quando combinato con altri valori. Ad esempio, è possibile usare "**adModeRead** oppure **adModeShareDenyNone** oppure **adModeRecursive**".|  
|**adModeShareDenyNone**|16|Consente ad altri utenti di aprire una connessione con le autorizzazioni. Impossibile negare l'accesso in lettura e in scrittura ad altri.|  
|**adModeShareDenyRead**|4|Impedisce ad altri l'apertura di una connessione con autorizzazioni di lettura.|  
|**adModeShareDenyWrite**|8|Impedisce ad altri l'apertura di una connessione con autorizzazioni di scrittura.|  
|**adModeShareExclusive**|12|Impedisce ad altri l'apertura di una connessione.|  
|**adModeUnknown**|0|Valore predefinito. Indica che le autorizzazioni non sono ancora state impostate o non possono essere determinate.|  
|**adModeWrite**|2|Indica le autorizzazioni di sola scrittura.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.ConnectMode.READ|  
|AdoEnums.ConnectMode.READWRITE|  
|(È disponibile un equivalente di AdoEnums.ConnectMode.RECURSIVE)|  
|AdoEnums.ConnectMode.SHAREDENYNONE|  
|AdoEnums.ConnectMode.SHAREDENYREAD|  
|AdoEnums.ConnectMode.SHAREDENYWRITE|  
|AdoEnums.ConnectMode.SHAREEXCLUSIVE|  
|AdoEnums.ConnectMode.UNKNOWN|  
|AdoEnums.ConnectMode.WRITE|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Proprietà Mode (ADO)](../../../ado/reference/ado-api/mode-property-ado.md)|[Metodo Open (record ADO)](../../../ado/reference/ado-api/open-method-ado-record.md)|  
|[Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)|[Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|
