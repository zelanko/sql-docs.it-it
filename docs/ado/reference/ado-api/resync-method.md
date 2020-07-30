---
title: Metodo di risincronizzazione | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::raw_Resync
- Fields::Resync
- Recordset20::Resync
- Fields::raw_Resync
helpviewer_keywords:
- Resync method [ADO]
ms.assetid: 73b355d4-a4c0-434b-bfc4-039b1c76b32e
author: rothja
ms.author: jroth
ms.openlocfilehash: 6907bfa9b83370074db9d9e2e522ed49d2c96e7e
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87243212"
---
# <a name="resync-method"></a>Metodo Resync
Aggiorna i dati nell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) corrente o nella raccolta di [campi](../../../ado/reference/ado-api/fields-collection-ado.md) di un oggetto [record](../../../ado/reference/ado-api/record-object-ado.md) dal database sottostante.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 facoltativo. Valore [AffectEnum](../../../ado/reference/ado-api/affectenum.md) che determina il numero di record su cui influirà il metodo di **Risincronizzazione** . Il valore predefinito è **adAffectAll**. Questo valore non è disponibile con il metodo **Resync** della raccolta **Fields** di un oggetto **record** .  
  
 *ResyncValues*  
 facoltativo. Valore [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) che specifica se i valori sottostanti vengono sovrascritti. Il valore predefinito è **adResyncAllValues**.  
  
## <a name="remarks"></a>Commenti  
  
## <a name="recordset"></a>recordset  
 Utilizzare il metodo **Resync** per risincronizzare i record del **Recordset** corrente con il database sottostante. Questa operazione è utile se si utilizza un cursore statico o di tipo "solo di tipo", ma si desidera visualizzare eventuali modifiche nel database sottostante.  
  
 Se si imposta la proprietà [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) su **adUseClient**, la **Risincronizzazione** è disponibile solo per gli oggetti **Recordset** non di sola lettura.  
  
 A differenza del metodo [Requery](../../../ado/reference/ado-api/requery-method.md) , il metodo **Resync** non esegue di nuovo il comando sottostante dell'oggetto **Recordset** . I nuovi record nel database sottostante non saranno visibili.  
  
 Se il tentativo di risincronizzazione non riesce a causa di un conflitto con i dati sottostanti (ad esempio, un record è stato eliminato da un altro utente), il provider restituisce avvisi alla raccolta [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) e si verifica un errore di run-time. Utilizzare la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterConflictingRecords**) e la proprietà [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) per individuare i record con conflitti.  
  
 Se vengono impostate le proprietà dinamiche della tabella e della [Risincronizzazione](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) [univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e il **Recordset** è il risultato dell'esecuzione di un'operazione di join su più tabelle, il metodo **Resync** eseguirà il comando specificato nella proprietà di **comando resync** solo nella tabella denominata nella proprietà **Unique Table** .  
  
## <a name="fields"></a>Campi  
 Utilizzare il metodo **Resync** per risincronizzare i valori della raccolta **Fields** di un oggetto **record** con l'origine dati sottostante. Questo metodo non ha effetto sulla proprietà [count](../../../ado/reference/ado-api/count-property-ado.md) .  
  
 Se *ResyncValues* è impostato su **adResyncAllValues** (valore predefinito), le proprietà [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [value](../../../ado/reference/ado-api/value-property-ado.md)e [OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) degli oggetti [Field](../../../ado/reference/ado-api/field-object.md) della raccolta sono sincronizzate. Se *ResyncValues* è impostato su **adResyncUnderlyingValues**, viene sincronizzata solo la proprietà **UnderlyingValue** .  
  
 Il valore della proprietà **status** per ogni oggetto **Field** al momento della chiamata influiscono anche sul comportamento della **Risincronizzazione**. Per gli oggetti **campo** con **Status** valori di stato **adFieldPendingUnknown** o **adFieldPendingInsert**, la **Risincronizzazione** non ha alcun effetto. Per i valori di **stato** di **adFieldPendingChange** o **adFieldPendingDelete**, la **Risincronizzazione** sincronizza i valori dei dati per i campi che esistono ancora nell'origine dati.  
  
 La **Risincronizzazione** non modifica i valori di **stato** degli oggetti **campo** a meno che non si verifichi un errore quando viene chiamata la **Risincronizzazione** . Se, ad esempio, il campo non esiste più, il provider restituirà un valore di **stato** appropriato per l'oggetto **campo** , ad esempio **adFieldDoesNotExist**. I valori di **stato** restituiti possono essere combinati in modo logico all'interno del valore della proprietà **status** .  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)  
    :::column-end:::
    :::column:::
        [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
    :::column-end:::
:::row-end:::

## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Resync (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Esempio di metodo Resync (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Proprietà UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
