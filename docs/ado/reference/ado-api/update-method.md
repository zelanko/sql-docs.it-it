---
title: Metodo Update | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Update
helpviewer_keywords:
- Update method [ADO]
ms.assetid: 6b2a9c31-1a7e-40db-8a53-30720d0f6cc1
author: rothja
ms.author: jroth
ms.openlocfilehash: 6c0d75e8f9fb6d11315e327edd6f7d064c13e063
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82759497"
---
# <a name="update-method"></a>Metodo Update
Salva le modifiche apportate alla riga corrente di un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) o alla raccolta di [campi](../../../ado/reference/ado-api/fields-collection-ado.md) di un oggetto [record](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parametri  
 *Fields*  
 Facoltativa. **Variant** che rappresenta un singolo nome o una matrice **Variant** che rappresenta nomi o posizioni ordinali del campo o dei campi che si desidera modificare.  
  
 *Valori*  
 Facoltativa. **Variant** che rappresenta un singolo valore o una matrice **Variant** che rappresenta i valori per il campo o i campi nel nuovo record.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="recordset"></a>recordset  
 Usare il metodo **Update** per salvare le modifiche apportate al record corrente di un oggetto **Recordset** , a partire dalla chiamata al metodo [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) o dalla modifica dei valori di campo in un record esistente. L'oggetto **Recordset** deve supportare gli aggiornamenti.  
  
 Per impostare i valori dei campi, effettuare una delle operazioni seguenti:  
  
-   Assegnare i valori alla proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) di un oggetto [campo](../../../ado/reference/ado-api/field-object.md) e chiamare il metodo **Update** .  
  
-   Passare un nome di campo e un valore come argomenti con la chiamata di **aggiornamento** .  
  
-   Passare una matrice di nomi di campo e una matrice di valori con la chiamata di **aggiornamento** .  
  
 Quando si utilizzano matrici di campi e valori, deve essere presente un numero uguale di elementi in entrambe le matrici. Inoltre, l'ordine dei nomi di campo deve corrispondere all'ordine dei valori di campo. Se il numero e l'ordine dei campi e i valori non corrispondono, si verificherà un errore.  
  
 Se l'oggetto **Recordset** supporta l'aggiornamento in batch, è possibile memorizzare nella cache più modifiche a uno o più record localmente fino a quando non si chiama il metodo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) . Se si modifica il record corrente o si aggiunge un nuovo record quando si chiama il metodo **UpdateBatch** , ADO chiamerà automaticamente il metodo **Update** per salvare le modifiche in sospeso apportate al record corrente prima di trasmettere le modifiche in batch al provider.  
  
 Se si passa dal record che si aggiunge o si modifica prima di chiamare il metodo **Update** , ADO chiamerà automaticamente **Update** per salvare le modifiche. È necessario chiamare il metodo [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) se si desidera annullare le modifiche apportate al record corrente o eliminare un record appena aggiunto.  
  
 Il record corrente rimane aggiornato dopo la chiamata al metodo **Update** .  
  
## <a name="record"></a>Record  
 Il metodo **Update** finalizza le aggiunte, le eliminazioni e gli aggiornamenti ai campi nella raccolta [Fields](../../../ado/reference/ado-api/fields-collection-ado.md) di un oggetto **record** .  
  
 Ad esempio, i campi eliminati con il metodo **Delete** vengono contrassegnati per l'eliminazione immediatamente ma rimangono nella raccolta. È necessario chiamare il metodo **Update** per eliminare effettivamente questi campi dalla raccolta del provider.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi Update e CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Esempio di metodi Update e CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Metodo AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
