---
title: Metodo di aggiornamento | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ae2645057670ba65a33bb8b5da238c7e01790ae9
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042237"
---
# <a name="update-method"></a>Metodo Update
Salva le modifiche apportate alla riga corrente di un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto, o il [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Update Fields, Values  
record.Fields.Update  
```  
  
#### <a name="parameters"></a>Parametri  
 *Fields*  
 Facoltativo. Oggetto **Variant** che rappresenta un singolo nome o una **Variant** matrice che rappresenta i nomi o posizione ordinale del campo o campi che si desidera modificare.  
  
 *Valori*  
 Facoltativo. Oggetto **Variant** che rappresenta un singolo valore, o una **Variant** matrice che rappresenta i valori per il campo o campi nel nuovo record.  
  
## <a name="remarks"></a>Note  
  
## <a name="recordset"></a>recordset  
 Usare il **Update** per salvare le modifiche apportate al record corrente di un **Recordset** oggetto dal momento della chiamata il [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) (metodo) oppure dopo aver modificato i valori di campo un record esistente. Il **Recordset** oggetto deve supportare gli aggiornamenti.  
  
 Per impostare i valori dei campi, eseguire una delle operazioni seguenti:  
  
-   Assegnare valori a un [campo](../../../ado/reference/ado-api/field-object.md) dell'oggetto [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà e chiamare il **Update** (metodo).  
  
-   Passare un nome di campo e il valore come argomenti con la **Update** chiamare.  
  
-   Passare una matrice di nomi di campo e una matrice di valori con il **Update** chiamare.  
  
 Quando si utilizzano matrici di valori e campi, deve esistere un numero uguale di elementi in entrambe le matrici. Inoltre, l'ordine dei nomi di campo deve corrispondere all'ordine dei valori dei campi. Se il numero e l'ordine dei campi e valori non corrispondono, si verifica un errore.  
  
 Se il **Recordset** oggetto supporta l'aggiornamento in batch, è possibile memorizzare nella cache più modifiche a uno o più record in locale fino a quando non si chiama il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) (metodo). Se si modifica il record corrente o aggiungere un nuovo record quando si chiama il **UpdateBatch** metodo, ADO chiama automaticamente il **Update** metodo per salvare le modifiche in sospeso per il record corrente prima di trasmettere le modifiche in batch al provider.  
  
 Se si sposta dal record si aggiunge o modifica prima di chiamare il **Update** metodo, verrà automaticamente chiamato **Update** per salvare le modifiche. È necessario chiamare il [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) metodo se si desidera annullare eventuali modifiche apportate al record corrente oppure eliminare il record appena aggiunto.  
  
 Il record corrente rimane invariato dopo aver chiamato il **Update** (metodo).  
  
## <a name="record"></a>Record  
 Il **Update** metodo Finalizza aggiunte, eliminazioni e aggiornamenti ai campi nel [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta di un **Record** oggetto.  
  
 Ad esempio, i campi eliminati con il **eliminare** metodo vengono contrassegnati per l'eliminazione immediatamente ma rimangono nell'insieme. Il **Update** metodo deve essere chiamato per eliminare effettivamente i campi dalla raccolta del provider.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Raccolta Fields (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)|[Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento metodi e CancelUpdate (VB)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vb.md)   
 [Aggiornamento metodi e CancelUpdate (VC + +)](../../../ado/reference/ado-api/update-and-cancelupdate-methods-example-vc.md)   
 [Metodo AddNew (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
