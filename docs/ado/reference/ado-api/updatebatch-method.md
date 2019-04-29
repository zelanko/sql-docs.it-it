---
title: Metodo UpdateBatch | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::UpdateBatch
- Recordset15::raw_UpdateBatch
helpviewer_keywords:
- UpdateBatch method [ADO]
ms.assetid: 23f9314c-b027-4a51-aeae-50caa2977740
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e39b7094b4b4543b60431f847ed792f18ace31f3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63040817"
---
# <a name="updatebatch-method"></a>Metodo UpdateBatch
Scrive tutti gli aggiornamenti in blocco in sospeso sul disco.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 Facoltativo. Un' [AffectEnum](../../../ado/reference/ado-api/affectenum.md) valore che indica il numero di record la **UpdateBatch** saranno influenzati dal metodo.  
  
 *PreserveStatus*  
 Facoltativo. Oggetto **booleana** valore che specifica se le modifiche locali, come indicato dal [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà, deve essere eseguito il commit. Se questo valore è impostato su **True**, il **stato** proprietà di ogni record rimane invariato dopo il completamento dell'aggiornamento.  
  
## <a name="remarks"></a>Note  
 Usare la **UpdateBatch** metodo quando si modifica un **Recordset** oggetto in modalità di aggiornamento batch per trasmettere tutte le modifiche apportate un **Recordset** oggetto nel database sottostante.  
  
 Se il **Recordset** oggetto supporta l'aggiornamento in batch, è possibile memorizzare nella cache più modifiche a uno o più record in locale fino a quando non si chiama il **UpdateBatch** (metodo). Se si modifica il record corrente o aggiungere un nuovo record quando si chiama il **UpdateBatch** metodo, ADO chiama automaticamente il [Update](../../../ado/reference/ado-api/update-method.md) metodo per salvare le modifiche in sospeso per il record corrente prima di trasmettere le modifiche in batch al provider. È consigliabile usare l'aggiornamento in blocco con un solo cursore statico o keyset.  
  
> [!NOTE]
>  Che specifica **adAffectGroup** come valore per questo parametro verrà generato un errore quando non sono presenti record visibili nell'attuale **Recordset** (ad esempio, un filtro per il quale nessun record corrispondente).  
  
 Se il tentativo di trasmettere le modifiche non riesce per qualsiasi o tutti i record a causa di un conflitto con i dati sottostanti (ad esempio, un record è già stato eliminato da un altro utente), il provider restituisce avvisi per i [errori](../../../ado/reference/ado-api/errors-collection-ado.md) raccolta e un oggetto si verifica l'errore di run-time. Usare la [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà (**adFilterAffectedRecords**) e il [stato](../../../ado/reference/ado-api/status-property-ado-recordset.md) proprietà per individuare i record con conflitti.  
  
 Per annullare tutte in sospeso aggiornamenti batch, usare il [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) (metodo).  
  
 Se il [tabella univoca](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) le proprietà dinamiche sono impostate e il **Recordset** è il risultato dell'esecuzione di un'operazione di JOIN in più tabelle, il l'esecuzione del **UpdateBatch** metodo in modo implicito è seguito dal [Risincronizza](../../../ado/reference/ado-api/resync-method.md) metodo, a seconda delle impostazioni del [Update Resync](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) proprietà.  
  
 L'ordine in cui i singoli aggiornamenti di un batch vengono eseguiti sull'origine dati non è necessariamente lo stesso l'ordine in cui sono stati eseguiti in locale **Recordset**. Ordine di aggiornamento dipende dal provider. Tenerne conto durante la codifica degli aggiornamenti che sono correlati tra loro, ad esempio i vincoli di chiave esterni per un inserimento o aggiornamento.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di UpdateBatch e CancelBatch (esempio di metodi (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Esempio UpdateBatch e CancelBatch metodi (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Proprietà LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)
