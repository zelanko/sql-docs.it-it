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
ms.openlocfilehash: 449d453ba8e1d27489fecaa8da56e76e1c85f313
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450983"
---
# <a name="clone-method-ado"></a>Metodo Clone (ADO)
Crea un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) duplicato da un oggetto **Recordset** esistente. Facoltativamente, specifica che il clone deve essere di sola lettura.  
  
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
 Facoltativo. Valore [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) che specifica il tipo di blocco del **Recordset**originale o un **Recordset**di sola lettura. I valori validi sono **adLockUnspecified** o **adLockReadOnly**.  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare il metodo **Clone** per creare più oggetti **Recordset** duplicati, soprattutto se si desidera mantenere più record correnti in un set di record specificato. L'utilizzo del metodo **Clone** è più efficiente rispetto alla creazione e all'apertura di un nuovo oggetto **Recordset** che utilizza la stessa definizione dell'originale.  
  
 La proprietà [Filter](../../../ado/reference/ado-api/filter-property.md) del **Recordset**originale, se presente, non verrà applicata al clone. Impostare la proprietà **Filter** del nuovo **Recordset** per filtrare i risultati. Il modo più semplice per copiare qualsiasi valore di **filtro** esistente consiste nell'assegnarlo direttamente, come indicato di seguito.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 Il record corrente di un clone appena creato viene impostato sul primo record.  
  
 Le modifiche apportate a un oggetto **Recordset** sono visibili in tutti i relativi cloni indipendentemente dal tipo di cursore. Tuttavia, dopo l'esecuzione di [Requery](../../../ado/reference/ado-api/requery-method.md) sul **Recordset**originale, i cloni non verranno più sincronizzati con quello originale.  
  
 La chiusura del **Recordset** originale non comporta la chiusura delle copie, né la chiusura di una copia chiude l'originale o una delle altre copie.  
  
 È possibile clonare solo un oggetto **Recordset** che supporta segnalibri. I valori dei segnalibri sono intercambiabili; ovvero, un riferimento a un segnalibro da un oggetto **Recordset** fa riferimento allo stesso record in uno dei relativi cloni.  
  
 In tutti i cloni dei **Recordset** verranno generati anche alcuni eventi **Recordset** attivati. Tuttavia, poiché il record corrente può variare tra **Recordset**clonati, gli eventi potrebbero non essere validi per il clone. Se ad esempio si modifica un valore di un campo, si verificherà un evento [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) nel **Recordset** modificato e in tutti i cloni. Il parametro *Fields* dell'evento **WillChangeField** di un **Recordset** clonato (in cui la modifica non è stata apportata) fa riferimento ai campi del record corrente del clone, che può essere un record diverso rispetto al record corrente del **Recordset** originale in cui si è verificata la modifica.  
  
 Nella tabella seguente viene fornito un elenco completo di tutti gli eventi **Recordset** . Indica se sono validi e attivati per tutti i cloni del recordset generati tramite il metodo **Clone** .  
  
|Event|Attivato nei cloni?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|No|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|No|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|No|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Sì|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|No|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Sì|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Sì|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Sì|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|No|  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Clone (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Esempio di metodo Clone (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Esempio del metodo Clone (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
