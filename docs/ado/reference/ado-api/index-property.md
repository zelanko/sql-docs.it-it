---
title: Proprietà index | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset21::Index
helpviewer_keywords:
- Index property
ms.assetid: 1c79e271-21ec-41a8-8163-c5e89f0001a7
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 21f8ec6ea0ed9cd1af8257dcd10b18f59903c929
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694800"
---
# <a name="index-property"></a>Proprietà Index
Indica il nome dell'indice attualmente attiva per un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Imposta o restituisce un **stringa** valore, ovvero il nome dell'indice.  
  
## <a name="remarks"></a>Note  
 L'indice denominato per il **indice** proprietà deve essere già stata dichiarata nella tabella di base sottostante il **Recordset** oggetto. Vale a dire, l'indice deve essere stata dichiarata a livello di codice come un ADOX [indice](../../../ado/reference/adox-api/index-object-adox.md) oggetto, o quando è stata creata la tabella di base.  
  
 Se non è possibile impostare l'indice, si verificherà un errore di run-time. Il **indice** vlastnost nelze nastavit nelle condizioni seguenti:  
  
-   All'interno di un [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) oppure **RecordsetChangeComplete** gestore dell'evento.  
  
-   Se il **Recordset** è ancora in esecuzione un'operazione (che può essere determinato mediante il [stato](../../../ado/reference/ado-api/state-property-ado.md) proprietà).  
  
-   Se un filtro è stato impostato la **Recordset** con il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà.  
  
 Il **indice** può sempre essere impostata correttamente se il **Recordset** viene chiuso, ma la **Recordset** non verrà aperto correttamente o l'indice non sarà possibile utilizzarlo, se la provider sottostante non supporta gli indici.  
  
 Se l'indice può essere impostato, può modificare la posizione della riga corrente. In questo modo un aggiornamento per il [esempio di AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) proprietà e genereranno il **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove ](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md), e [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) gli eventi.  
  
 Se l'indice può essere impostato e il [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) è di proprietà **adLockPessimistic** oppure **adLockOptimistic**, quindi implicita [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) operazione viene eseguita. Rilascia i gruppi interessati e correnti. Qualsiasi filtro esistente viene rilasciato e viene modificata la posizione della riga corrente sulla prima riga del riordinati **Recordset**.  
  
 Il **indice** proprietà viene utilizzata in combinazione con la [Seek](../../../ado/reference/ado-api/seek-method.md) (metodo). Se il provider sottostante non supporta il **indice** proprietà e pertanto il **Seek** metodo, è consigliabile usare il [trovare](../../../ado/reference/ado-api/find-method-ado.md) metodo invece. Determinare se il **Recordset** oggetto supporta gli indici con il [supporta](../../../ado/reference/ado-api/supports-method.md)**(adIndex)** (metodo).  
  
 L'elemento predefinito **indice** proprietà non è correlata a dinamica [Optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) proprietà, anche se entrambe vengono utilizzate per gli indici.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Seek e esempio di proprietà indice (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Oggetto Index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Metodo Seek](../../../ado/reference/ado-api/seek-method.md)
