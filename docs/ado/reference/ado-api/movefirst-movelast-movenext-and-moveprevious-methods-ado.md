---
title: Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (ADO) | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 83e216f15da49150481af18ee98aac1f604b2394
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707477"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (ADO)
Sposta il primo, ultimo, successivo o precedente record in un oggetto specificato [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) specificato e ne fanno il record corrente.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>Note  
 Usare la **MoveFirst** metodo per spostare la posizione corrente del primo record la **Recordset**.  
  
 Usare la **MoveLast** metodo per spostare la posizione corrente all'ultimo record nelle **Recordset**. Il **Recordset** oggetto deve supportare lo spostamento del cursore con le versioni precedenti o i segnalibri; in caso contrario, la chiamata al metodo genererà un errore.  
  
 Una chiamata a uno **MoveFirst** oppure **MoveLast** quando la **Recordset** è vuota (entrambi **BOF** e **EOF** sussistono) genera un errore.  
  
 Usare la **MoveNext** metodo per spostare il record corrente posizionare un record di inoltro (verso il basso il **Recordset**). Se l'ultimo record corrisponde al record corrente e si chiama il **MoveNext** metodo, ADO imposta il record corrente alla posizione successiva all'ultimo record nelle **Recordset** ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) è **True**). Tenta di spostarsi in avanti quando le **EOF** proprietà è già **True** genera un errore.  
  
 In ADO 2.5 e versioni successiva, quando il **Recordset** è stato filtrato o ordinato e i dati del record corrente viene modificati, la chiamata il **MoveNext** metodo sposta i record di cursore due inoltrare del record corrente . Questo avviene perché quando viene modificato il record corrente, il record successivo diventa il nuovo record corrente. La chiamata **MoveNext** dopo la modifica si sposta il cursore al record successivo dal nuovo record corrente. Ciò è diverso da quello in ADO 2.1 e versioni precedenti. Nelle versioni precedenti, la modifica dei dati di un record corrente nella ordinata o filtrata **Recordset** non modifica la posizione del record corrente, e **MoveNext** sposta il cursore sul record successivo immediatamente dopo il record corrente.  
  
 Usare la **MovePrevious** metodo per spostare il record corrente posizionare un record con le versioni precedenti (verso l'alto il **Recordset**). Il **Recordset** oggetto deve supportare lo spostamento del cursore con le versioni precedenti o i segnalibri; in caso contrario, la chiamata al metodo genererà un errore. Se il primo record corrisponde al record corrente e si chiama il **MovePrevious** metodo, ADO imposta il record corrente alla posizione prima del primo record la **Recordset** ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)viene **True**). Tenta di spostarsi con le versioni precedenti quando le **BOF** proprietà è già **True** genera un errore. Se il **Recordset** objekt nepodporuje segnalibri o uno spostamento del cursore con le versioni precedenti, il **MovePrevious** metodo genererà un errore.  
  
 Se il **Recordset** è forward-only e si desidera supportare lo scorrimento in avanti e indietro, è possibile utilizzare il [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) proprietà per creare una cache di record che supporta lo spostamento del cursore con le versioni precedenti tramite il [spostare](../../../ado/reference/ado-api/move-method-ado.md) (metodo). Poiché i record memorizzati nella cache vengono caricati in memoria, è consigliabile evitare la memorizzazione nella cache più record del necessario. È possibile chiamare il **MoveFirst** metodo in un tipo forward-only **Recordset** oggetto; questa operazione può causare il provider eseguire nuovamente il comando che ha generato il **Recordset** oggetto .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (esempio di metodi (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (esempio di metodi (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst, MoveLast, MoveNext e MovePrevious esempio di metodi (VC + +)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Metodo Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [Metodo MoveRecord (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
