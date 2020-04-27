---
title: Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e5f0cdacc6e0d7e5512dbc259815e5b9562c9b68
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918116"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)
Passa al record primo, ultimo, successivo o precedente in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) specificato e fa in modo che registri il record corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **MoveFirst** per spostare la posizione del record corrente nel primo record del **Recordset**.  
  
 Usare il metodo **MoveLast** per spostare la posizione del record corrente nell'ultimo record del **Recordset**. L'oggetto **Recordset** deve supportare i segnalibri o lo spostamento all'indietro del cursore. in caso contrario, la chiamata al metodo genererà un errore.  
  
 Una chiamata a **MoveFirst** o **MoveLast** quando il **Recordset** è vuoto (sia **BOF** che **EOF** sono true) genera un errore.  
  
 Utilizzare il metodo **MoveNext** per spostare in avanti la posizione del record corrente di un record (verso la parte inferiore del **Recordset**). Se l'ultimo record è il record corrente e si chiama il metodo **MoveNext** , ADO imposta il record corrente sulla posizione dopo l'ultimo record nel **Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **true**). Un tentativo di andare avanti quando la proprietà **EOF** è già **true** genera un errore.  
  
 In ADO 2,5 e versioni successive, quando il **Recordset** è stato filtrato o ordinato e i dati del record corrente vengono modificati, la chiamata al metodo **MoveNext** sposta il cursore a due record in avanti rispetto al record corrente. Questo è dovuto al fatto che quando il record corrente viene modificato, il record successivo diventa il nuovo record corrente. La chiamata a **MoveNext** dopo la modifica sposta il cursore di un record in base al nuovo record corrente. Si tratta di un comportamento diverso rispetto a ADO 2,1 e versioni precedenti. In queste versioni precedenti, la modifica dei dati di un record corrente nel **Recordset** ordinato o filtrato non comporta la modifica della posizione del record corrente e **MoveNext** sposta il cursore sul record successivo subito dopo il record corrente.  
  
 Usare il metodo **MovePrevious** per spostare la posizione del record corrente di un record indietro (verso la parte superiore del **Recordset**). L'oggetto **Recordset** deve supportare i segnalibri o lo spostamento all'indietro del cursore. in caso contrario, la chiamata al metodo genererà un errore. Se il primo record è il record corrente e si chiama il metodo **MovePrevious** , ADO imposta il record corrente sulla posizione prima del primo record nel **Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **true**). Un tentativo di spostarsi all'indietro quando la proprietà **BOF** è già **true** genera un errore. Se l'oggetto **Recordset** non supporta segnalibri o movimenti di cursore a ritroso, il metodo **MovePrevious** genererà un errore.  
  
 Se il **Recordset** è di sola trasmissione e si desidera supportare lo scorrimento avanti e indietro, è possibile utilizzare la proprietà [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) per creare una cache di record che supporti lo spostamento all'indietro del cursore tramite il metodo [Move](../../../ado/reference/ado-api/move-method-ado.md) . Poiché i record memorizzati nella cache vengono caricati in memoria, è consigliabile evitare di memorizzare nella cache più record del necessario. È possibile chiamare il metodo **MoveFirst** in un oggetto **Recordset** di sola trasmissione; in questo modo, il provider può eseguire di nuovo il comando che ha generato l'oggetto **Recordset** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Esempio di metodi MoveFirst, MoveLast, MoveNext e MovePrevious (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [Esempio di metodi MoveFirst, MoveLast, MoveNext e MovePrevious (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [Esempio di metodi MoveFirst, MoveLast, MoveNext e MovePrevious (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Metodo Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Metodo MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
