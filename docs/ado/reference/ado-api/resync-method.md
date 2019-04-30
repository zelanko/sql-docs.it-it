---
title: Metodo Resync | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 68ca8ac6d223100f437a7ba0ca8bf7776953d40a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062269"
---
# <a name="resync-method"></a>Metodo Resync
Aggiorna i dati nell'attuale [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, o [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto, dal database sottostante.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Recordset.Resync AffectRecords, ResyncValues Record.Fields.Resync ResyncValues  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 Facoltativo. Un' [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valore che determina il numero di record la **Risincronizza** saranno influenzati dal metodo. Il valore predefinito è **adAffectAll**. Questo valore non è disponibile con la **Risincronizza** metodo per il **campi** raccolta di un **Record** oggetto.  
  
 *ResyncValues*  
 Facoltativo. Oggetto [ResyncEnum](../../../ado/reference/ado-api/resyncenum.md) valore che specifica se i valori sottostanti vengono sovrascritti. Il valore predefinito è **adResyncAllValues**.  
  
## <a name="remarks"></a>Note  
  
## <a name="recordset"></a>recordset  
 Usare la **Risincronizza** metodo risincronizzare i record nell'attuale **Recordset** con il database sottostante. Ciò è utile se si usa un cursore statico o di tipo forward-only, ma si desidera visualizzare tutte le modifiche nel database sottostante.  
  
 Se si imposta la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) proprietà **adUseClient**, **Risincronizza** è disponibile solo per non di sola lettura **Recordset** oggetti.  
  
 A differenza del [rieseguire una query](../../../ado/reference/ado-api/requery-method.md) metodo, il **Risincronizza** metodo non viene nuovamente eseguito il **Recordset** sottostante del comando. Nuovi record nel database sottostante non saranno visibili.  
  
 Se il tentativo di risincronizzare ha esito negativo a causa di un conflitto con i dati sottostanti (ad esempio, un record è stato eliminato da un altro utente), il provider restituisce avvisi per i [errori](../../../ado/reference/ado-api/errors-collection-ado.md) si verifica un errore di run-time e raccolta. Usare la [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà (**adFilterConflictingRecords**) e il [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà per individuare i record con conflitti.  
  
 Se il [tabelle univoche](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e [Resync Command](../../../ado/reference/ado-api/resync-command-property-dynamic-ado.md) le proprietà dinamiche sono impostate e il **Recordset** è il risultato dell'esecuzione di un'operazione di JOIN in più tabelle, allora il  **Risincronizza** metodo eseguirà il comando specificato nella **Resync Command** proprietà solo per la tabella denominata nel **tabella univoca** proprietà.  
  
## <a name="fields"></a>Campi  
 Usare la **Risincronizza** metodo risincronizzare i valori del **campi** raccolta di un **Record** oggetto con l'origine dati sottostante. Il [conteggio](../../../ado/reference/ado-api/count-property-ado.md) proprietà non è interessata da questo metodo.  
  
 Se *ResyncValues* è impostata su **adResyncAllValues** (valore predefinito), il [UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md), [valore](../../../ado/reference/ado-api/value-property-ado.md), e [ Esempio di OriginalValue](../../../ado/reference/ado-api/originalvalue-property-ado.md) delle proprietà di [campo](../../../ado/reference/ado-api/field-object.md) sincronizzazione degli oggetti nella raccolta. Se *ResyncValues* è impostata su **adResyncUnderlyingValues**, solo il **UnderlyingValue** proprietà è sincronizzata.  
  
 Il valore della **lo stato** proprietà per ogni **campo** oggetto al momento della chiamata influisce anche sul comportamento di **Risincronizza**. Per **campo** gli oggetti che hanno **stato** valori di **su adFieldPendingUnknown** oppure **adFieldPendingInsert**, **Resync**  non ha alcun effetto. Per **lo stato** i valori di **uguali a adFieldPendingChange** oppure **adFieldPendingDelete**, **Risincronizza** Sincronizza i valori dei dati per i campi che esiste ancora nell'origine dati.  
  
 **Risincronizza** non modificherà **stato** valori di **campo** oggetti a meno che non si verifica un errore quando **Risincronizza** viene chiamato. Ad esempio, se il campo non esiste più, il provider restituisce un'apposita **lo stato** valore per il **campo** dell'oggetto, ad esempio **adFieldDoesNotExist**. Restituiti **lo stato** valori possono essere combinati in modo logico all'interno del valore della **stato** proprietà.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Risincronizzare l'esempio di metodo (VB)](../../../ado/reference/ado-api/resync-method-example-vb.md)   
 [Risincronizzare l'esempio di metodo (VC + +)](../../../ado/reference/ado-api/resync-method-example-vc.md)   
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Proprietà UnderlyingValue](../../../ado/reference/ado-api/underlyingvalue-property.md)
