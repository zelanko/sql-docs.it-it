---
description: Proprietà Index
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 80d15588279e584ec4d63d4336239952f22405cc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443463"
---
# <a name="index-property"></a>Proprietà Index
Indica il nome dell'indice attualmente attivo per un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) .  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Imposta o restituisce un valore **stringa** che rappresenta il nome dell'indice.  
  
## <a name="remarks"></a>Osservazioni  
 L'indice denominato dalla proprietà **index** deve essere stato dichiarato in precedenza nella tabella di base sottostante l'oggetto **Recordset** . Ovvero è necessario che l'indice sia stato dichiarato a livello di codice come oggetto [Indice](../../../ado/reference/adox-api/index-object-adox.md) ADOX o quando è stata creata la tabella di base.  
  
 Se non è possibile impostare l'indice, si verificherà un errore di run-time. Impossibile impostare la proprietà **index** nelle condizioni seguenti:  
  
-   All'interno di un gestore dell'evento [WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) o **RecordsetChangeComplete** .  
  
-   Se il **Recordset** sta ancora eseguendo un'operazione (che può essere determinata dalla proprietà [state](../../../ado/reference/ado-api/state-property-ado.md) ).  
  
-   Se è stato impostato un filtro sul **Recordset** con la proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) .  
  
 La proprietà **index** può sempre essere impostata correttamente se il **Recordset** è chiuso, ma il **Recordset** non verrà aperto correttamente oppure l'indice non sarà utilizzabile se il provider sottostante non supporta gli indici.  
  
 Se è possibile impostare l'indice, la posizione della riga corrente potrebbe cambiare. Verrà generato un aggiornamento della proprietà [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e verranno attivati gli eventi **WillChangeRecordset**, **RecordsetChangeComplete**, [WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)e [MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md) .  
  
 Se è possibile impostare l'indice e la proprietà [LockType](../../../ado/reference/ado-api/locktype-property-ado.md) è **adLockPessimistic** o **adLockOptimistic**, viene eseguita un'operazione [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) implicita. Questa operazione rilascia i gruppi correnti e interessati. Tutti i filtri esistenti vengono rilasciati e la posizione della riga corrente viene modificata nella prima riga del **Recordset**riordinato.  
  
 La proprietà **index** viene utilizzata insieme al metodo [Seek](../../../ado/reference/ado-api/seek-method.md) . Se il provider sottostante non supporta la proprietà **index** e quindi il metodo **Seek** , provare a usare il metodo [Find](../../../ado/reference/ado-api/find-method-ado.md) . Determinare se l'oggetto **Recordset** supporta gli indici con il metodo [Supports](../../../ado/reference/ado-api/supports-method.md)**(adIndex)** .  
  
 La proprietà di **Indice** incorporata non è correlata alla proprietà dinamica [optimize](../../../ado/reference/ado-api/optimize-property-dynamic-ado.md) , sebbene entrambi gestiscano gli indici.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Seek e proprietà index (VB)](../../../ado/reference/ado-api/seek-method-and-index-property-example-vb.md)   
 [Oggetto index (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Seek (metodo)](../../../ado/reference/ado-api/seek-method.md)
