---
title: ExecuteOptionEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ExecuteOptionEnum
helpviewer_keywords:
- ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 589519e7c4a075d5fb06b5f2640d48e5d4ed898d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66695267"
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
Specifica il modo in cui un provider di eseguire un comando.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|Indica che il comando deve essere eseguito in modo asincrono.<br /><br /> Questo valore non può essere combinato con il [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valore **adCmdTableDirect**.|  
|**adAsyncFetch**|0x20|Indica che le rimanenti righe dopo la quantità iniziale specificato nel [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) proprietà deve essere recuperata in modo asincrono.|  
|**adAsyncFetchNonBlocking**|0x40|Indica che il thread principale si blocca mai durante il recupero. Se la riga richiesta non è stata recuperata, alla riga corrente verrà spostato automaticamente alla fine del file.<br /><br /> Se si apre un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) da un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) contenenti un oggetto archiviato in modo permanente **Recordset**, **adAsyncFetchNonBlocking** non avrà un effetto. l'operazione verrà ritentata sincrona e bloccante.<br /><br /> **adAsynchFetchNonBlocking** non ha alcun effetto quando il [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) opzione viene usata per aprire la **Recordset**.|  
|**adExecuteNoRecords**|0x80|Indica che il testo del comando è un comando o stored procedure che non restituiscono righe (ad esempio, un comando che viene inserito solo dati). Se tutte le righe vengono recuperate, vengono eliminati e non viene restituiti.<br /><br /> **adExecuteStream** può solo essere passato come parametro facoltativo per il **comandi** oppure **Esegui connessione** (metodo).|  
|**adExecuteStream**|0x400|Indica che i risultati di un'esecuzione del comando devono essere restituiti come flusso.<br /><br /> **adExecuteStream** può solo essere passato come parametro facoltativo per il **Command Execute** (metodo).|  
|**adExecuteRecord**||Indica che il **CommandText** è un comando o stored procedure che restituisce una singola riga che deve essere restituita come una **Record** oggetto.|  
|**adOptionUnspecified**|-1|Indica che il comando non è specificato.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo Execute (comando ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Metodo Execute (connessione ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Metodo Requery](../../../ado/reference/ado-api/requery-method.md)|
