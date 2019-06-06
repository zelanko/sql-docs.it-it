---
title: Metodo Move (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c7b99a0848101ca0fad4844c51e44f1ccc628cd6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707606"
---
# <a name="move-method-ado"></a>Metodo Move (ADO)
Sposta la posizione del record corrente in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parametri  
 *NumRecords*  
 Signed **lungo** espressione che specifica il numero di record che si sposta la posizione del record corrente.  
  
 *Start*  
 Facoltativo. Oggetto **stringa** valore oppure **Variant** che restituisca un segnalibro. È anche possibile usare una [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) valore.  
  
## <a name="remarks"></a>Note  
 Il **spostare** metodo è supportato su tutti **Recordset** oggetti.  
  
 Se il *NumRecords* argomento è maggiore di zero, la posizione corrente si sposta in avanti (verso la fine del **Recordset**). Se *NumRecords* è minore di zero, la posizione corrente si sposta all'indietro (verso l'inizio della **Recordset**).  
  
 Se il **spostare** chiamata Sposta la posizione del record corrente in un punto prima del primo record, ADO imposta il record corrente alla posizione prima del primo record del recordset ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **True** ). Tenta di spostarsi con le versioni precedenti quando le **BOF** proprietà è già **True** genera un errore.  
  
 Se il **spostare** chiamata Sposta la posizione corrente in un punto dopo l'ultimo record, ADO imposta il record corrente alla posizione successiva all'ultimo record del recordset ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **True** ). Tenta di spostarsi in avanti quando le **EOF** proprietà è già **True** genera un errore.  
  
 Chiama il **spostare** metodo da un oggetto vuoto **Recordset** oggetto genera un errore.  
  
 Se si passa il *avviare* argomento, lo spostamento è relativo al record con il segnalibro, presupponendo che le **Recordset** oggetto supporta i segnalibri. Se non specificato, lo spostamento è relativo al record corrente.  
  
 Se si usa la [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) proprietà da memorizzare localmente i record dal provider, passando un *NumRecords* argomento che sposta la posizione corrente all'esterno del gruppo corrente di record memorizzati nella cache forza ADO per recuperare un nuovo gruppo di record, a partire dal record di destinazione. Il **CacheSize** proprietà determina la dimensione del gruppo appena recuperato e il record di destinazione è il primo record recuperati.  
  
 Se il **Recordset** oggetto è forward-only, è comunque possibile passare un *NumRecords* argomento è minore di zero, fornito la destinazione è all'interno del set corrente di record memorizzati nella cache. Se il **spostare** chiamata Sposta la posizione del record corrente in un record prima del primo record memorizzati nella cache, si verificherà un errore. Di conseguenza, è possibile usare una cache di record che supporta lo scorrimento completo su un provider che supporta solo scorrimento in avanti. Poiché i record memorizzati nella cache vengono caricati in memoria, è consigliabile evitare la memorizzazione nella cache più record rispetto al necessario. Anche se un tipo forward-only **Recordset** supporta l'oggetto con le versioni precedenti si sposta in questo modo, la chiamata il [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) metodo su qualsiasi tipo forward-only **Recordset** oggetto verrà comunque Genera un errore.  
  
> [!NOTE]
>  Supporto per lo spostamento all'indietro nel forward-only **Recordset** non è prevedibile, a seconda del provider. Se il record corrente è stato posizionato dopo l'ultimo record nel **Recordset**, **spostare** con le versioni precedenti può non comportare la posizione corrente corretta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Esempio di metodo Move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Esempio di metodo Move (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Metodo MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
