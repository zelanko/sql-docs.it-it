---
description: Metodo UpdateBatch
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3f0a730a64a34e13f5a7554ecb700ab1e555a77d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441603"
---
# <a name="updatebatch-method"></a>Metodo UpdateBatch
Scrive tutti gli aggiornamenti batch in sospeso sul disco.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.UpdateBatch AffectRecords, PreserveStatus  
```  
  
#### <a name="parameters"></a>Parametri  
 *AffectRecords*  
 Facoltativo. Valore [AffectEnum](../../../ado/reference/ado-api/affectenum.md) che indica il numero di record su cui avrà effetto il metodo **UpdateBatch** .  
  
 *PreserveStatus*  
 Facoltativo. Valore **booleano** che specifica se è necessario eseguire il commit delle modifiche locali, come indicato dalla proprietà [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) . Se questo valore è impostato su **true**, la proprietà **status** di ogni record rimarrà invariata al termine dell'aggiornamento.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare il metodo **UpdateBatch** quando si modifica un oggetto **Recordset** in modalità di aggiornamento batch per trasmettere tutte le modifiche apportate in un oggetto **Recordset** al database sottostante.  
  
 Se l'oggetto **Recordset** supporta l'aggiornamento in batch, è possibile memorizzare nella cache più modifiche a uno o più record localmente fino a quando non si chiama il metodo **UpdateBatch** . Se si modifica il record corrente o si aggiunge un nuovo record quando si chiama il metodo **UpdateBatch** , ADO chiamerà automaticamente il metodo [Update](../../../ado/reference/ado-api/update-method.md) per salvare le modifiche in sospeso apportate al record corrente prima di trasmettere le modifiche in batch al provider. È consigliabile utilizzare l'aggiornamento batch solo con un keyset o un cursore statico.  
  
> [!NOTE]
>  Se si specifica **adAffectGroup** come valore per questo parametro, verrà generato un errore quando nel **Recordset** corrente non sono presenti record visibili, ad esempio un filtro per il quale non è presente alcun record corrispondente.  
  
 Se il tentativo di trasmettere le modifiche non riesce per uno o tutti i record a causa di un conflitto con i dati sottostanti (ad esempio, un record è già stato eliminato da un altro utente), il provider restituisce avvisi alla raccolta degli [errori](../../../ado/reference/ado-api/errors-collection-ado.md) e si verifica un errore di run-time. Utilizzare la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) (**adFilterAffectedRecords**) e la proprietà [status](../../../ado/reference/ado-api/status-property-ado-recordset.md) per individuare i record con conflitti.  
  
 Per annullare tutti gli aggiornamenti batch in sospeso, usare il metodo [CancelBatch](../../../ado/reference/ado-api/cancelbatch-method-ado.md) .  
  
 Se le proprietà dinamiche della [tabella](../../../ado/reference/ado-api/unique-table-unique-schema-unique-catalog-properties-dynamic-ado.md) e della [Risincronizzazione degli aggiornamenti](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) sono impostate e il **Recordset** è il risultato dell'esecuzione di un'operazione di join su più tabelle, l'esecuzione del metodo **UpdateBatch** viene seguita in modo implicito dal metodo di [Risincronizzazione](../../../ado/reference/ado-api/resync-method.md) , a seconda delle impostazioni della proprietà [Aggiorna risincronizzazione](../../../ado/reference/ado-api/update-resync-property-dynamic-ado.md) .  
  
 L'ordine in cui i singoli aggiornamenti di un batch vengono eseguiti sull'origine dati non corrisponde necessariamente all'ordine in cui sono stati eseguiti sul **Recordset**locale. L'ordine di aggiornamento dipende dal provider. Prendere in considerazione questo problema quando si codificano gli aggiornamenti correlati tra loro, ad esempio vincoli di chiave esterna per un inserimento o un aggiornamento.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi UpdateBatch e CancelBatch (VB)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vb.md)   
 [Esempio di metodi UpdateBatch e CancelBatch (VC + +)](../../../ado/reference/ado-api/updatebatch-and-cancelbatch-methods-example-vc.md)   
 [Metodo CancelBatch (ADO)](../../../ado/reference/ado-api/cancelbatch-method-ado.md)   
 [Metodo Clear (ADO)](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Proprietà LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)
