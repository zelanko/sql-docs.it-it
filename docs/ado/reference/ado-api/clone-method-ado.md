---
description: Metodo Clone (ADO)
title: Metodo Clone (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: rothja
ms.author: jroth
ms.openlocfilehash: c91960975b04e5c09cf2745e1bb77e7b343dbd2e
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88776250"
---
# <a name="clone-method-ado"></a>Metodo Clone (ADO)
Crea un oggetto [Recordset](./recordset-object-ado.md) duplicato da un oggetto **Recordset** esistente. Facoltativamente, specifica che il clone deve essere di sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un riferimento a un oggetto **Recordset** .  
  
#### <a name="parameters"></a>Parametri  
 *rstDuplicate*  
 Variabile oggetto che identifica l'oggetto **Recordset** duplicato da creare.  
  
 *rstOriginal*  
 Variabile oggetto che identifica l'oggetto **Recordset** da duplicare.  
  
 *LockType*  
 Facoltativa. Valore [LockTypeEnum](./locktypeenum.md) che specifica il tipo di blocco del **Recordset**originale o un **Recordset**di sola lettura. I valori validi sono **adLockUnspecified** o **adLockReadOnly**.  
  
## <a name="remarks"></a>Commenti  
 Utilizzare il metodo **Clone** per creare più oggetti **Recordset** duplicati, soprattutto se si desidera mantenere più record correnti in un set di record specificato. L'utilizzo del metodo **Clone** è più efficiente rispetto alla creazione e all'apertura di un nuovo oggetto **Recordset** che utilizza la stessa definizione dell'originale.  
  
 La proprietà [Filter](./filter-property.md) del **Recordset**originale, se presente, non verrà applicata al clone. Impostare la proprietà **Filter** del nuovo **Recordset** per filtrare i risultati. Il modo più semplice per copiare qualsiasi valore di **filtro** esistente consiste nell'assegnarlo direttamente, come indicato di seguito.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 Il record corrente di un clone appena creato viene impostato sul primo record.  
  
 Le modifiche apportate a un oggetto **Recordset** sono visibili in tutti i relativi cloni indipendentemente dal tipo di cursore. Tuttavia, dopo l'esecuzione di [Requery](./requery-method.md) sul **Recordset**originale, i cloni non verranno più sincronizzati con quello originale.  
  
 La chiusura del **Recordset** originale non comporta la chiusura delle copie, né la chiusura di una copia chiude l'originale o una delle altre copie.  
  
 È possibile clonare solo un oggetto **Recordset** che supporta segnalibri. I valori dei segnalibri sono intercambiabili; ovvero, un riferimento a un segnalibro da un oggetto **Recordset** fa riferimento allo stesso record in uno dei relativi cloni.  
  
 In tutti i cloni dei **Recordset** verranno generati anche alcuni eventi **Recordset** attivati. Tuttavia, poiché il record corrente può variare tra **Recordset**clonati, gli eventi potrebbero non essere validi per il clone. Se ad esempio si modifica un valore di un campo, si verificherà un evento [WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md) nel **Recordset** modificato e in tutti i cloni. Il parametro *Fields* dell'evento **WillChangeField** di un **Recordset** clonato (in cui la modifica non è stata apportata) fa riferimento ai campi del record corrente del clone, che può essere un record diverso rispetto al record corrente del **Recordset** originale in cui si è verificata la modifica.  
  
 Nella tabella seguente viene fornito un elenco completo di tutti gli eventi **Recordset** . Indica se sono validi e attivati per tutti i cloni del recordset generati tramite il metodo **Clone** .  
  
|Event|Attivato nei cloni?|  
|-----------|--------------------------|  
|[EndOfRecordset](./endofrecordset-event-ado.md)|No|  
|[FetchComplete](./fetchcomplete-event-ado.md)|No|  
|[FetchProgress](./fetchprogress-event-ado.md)|No|  
|[FieldChangeComplete](./willchangefield-and-fieldchangecomplete-events-ado.md)|Sì|  
|[MoveComplete](./willmove-and-movecomplete-events-ado.md)|No|  
|[RecordChangeComplete](./willchangerecord-and-recordchangecomplete-events-ado.md)|Sì|  
|[RecordsetChangeComplete](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillChangeField](./willchangefield-and-fieldchangecomplete-events-ado.md)|Sì|  
|[WillChangeRecord](./willchangerecord-and-recordchangecomplete-events-ado.md)|Sì|  
|[WillChangeRecordset](./willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillMove](./willmove-and-movecomplete-events-ado.md)|No|  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Clone (VB)](./clone-method-example-vb.md)   
 [Esempio di metodo Clone (VBScript)](./clone-method-example-vbscript.md)   
 [Esempio del metodo Clone (VC++)](./clone-method-example-vc.md)