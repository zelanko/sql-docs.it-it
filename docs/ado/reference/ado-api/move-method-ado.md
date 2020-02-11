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
ms.openlocfilehash: 4d76f239094185af7a3e940201b3f99132c0194a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918190"
---
# <a name="move-method-ado"></a>Metodo Move (ADO)
Sposta la posizione del record corrente in un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parametri  
 *NumRecords*  
 Espressione **Long** con segno che specifica il numero di record spostati dalla posizione corrente del record.  
  
 *Inizia*  
 Facoltativa. Valore **stringa** o **variante** che restituisce un segnalibro. È anche possibile usare un valore [BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Il metodo **Move** è supportato in tutti gli oggetti **Recordset** .  
  
 Se l'argomento *NumRecords* è maggiore di zero, la posizione corrente del record viene spostata in avanti (verso la fine del **Recordset**). Se *NumRecords* è minore di zero, la posizione corrente del record viene spostata indietro (verso l'inizio del **Recordset**).  
  
 Se la chiamata di **spostamento** sposta la posizione del record corrente in un punto prima del primo record, ADO imposta il record corrente sulla posizione prima del primo record nel recordset ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **true**). Un tentativo di spostarsi all'indietro quando la proprietà **BOF** è già **true** genera un errore.  
  
 Se la chiamata di **spostamento** sposta la posizione del record corrente in un punto successivo all'ultimo record, ADO imposta il record corrente sulla posizione dopo l'ultimo record nel recordset ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **true**). Un tentativo di andare avanti quando la proprietà **EOF** è già **true** genera un errore.  
  
 Se si chiama il metodo **Move** da un oggetto **Recordset** vuoto, viene generato un errore.  
  
 Se si passa l'argomento *Start* , lo spostamento è relativo al record con questo segnalibro, supponendo che l'oggetto **Recordset** supporti i segnalibri. Se non specificato, lo spostamento è relativo al record corrente.  
  
 Se si usa la proprietà [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) per memorizzare nella cache locale i record del provider, il passaggio di un argomento *NumRecords* che sposta la posizione del record corrente all'esterno del gruppo corrente di record memorizzati nella cache impone a ADO di recuperare un nuovo gruppo di record, a partire dal record di destinazione. La proprietà **CacheSize** determina le dimensioni del gruppo appena recuperato e il record di destinazione è il primo record recuperato.  
  
 Se l'oggetto **Recordset** è inoltrato, un utente può comunque passare un argomento *NumRecords* minore di zero, purché la destinazione si trovi all'interno del set corrente di record memorizzati nella cache. Se la chiamata di **spostamento** sposta la posizione del record corrente in un record prima del primo record memorizzato nella cache, si verificherà un errore. Pertanto, è possibile utilizzare una cache di record che supporta lo scorrimento completo su un provider che supporta solo lo scorrimento in futuro. Poiché i record memorizzati nella cache vengono caricati in memoria, è consigliabile evitare di memorizzare nella cache più record del necessario. Anche se un oggetto **Recordset** di tipo solo avanti supporta lo spostamento indietro in questo modo, la chiamata al metodo [MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) su un oggetto **Recordset** di tipo solo avanti genererà comunque un errore.  
  
> [!NOTE]
>  Il supporto per lo stato di avanzamento all'indietro in un **Recordset** di tipo "solo" non è prevedibile, a seconda del provider. Se il record corrente è stato posizionato dopo l'ultimo record del **Recordset**, lo **spostamento** all'indietro potrebbe non comportare la posizione corrente corretta.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Move (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Esempio di metodo Move (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Esempio di metodo Move (VC + +)](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Metodo MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
