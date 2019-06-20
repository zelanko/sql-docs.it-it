---
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fbeedf9e56c1f0606a7c8f842baedc9d11ad3929
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698800"
---
# <a name="clone-method-ado"></a>Metodo Clone (ADO)
Crea un duplicato [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto da un oggetto esistente **Recordset** oggetto. Facoltativamente, specifica che il clone sia di sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **Recordset** il riferimento all'oggetto.  
  
#### <a name="parameters"></a>Parametri  
 *rstDuplicate*  
 Una variabile oggetto che identifica il duplicato **Recordset** oggetto da creare.  
  
 *rstOriginal*  
 Una variabile oggetto che identifica la **Recordset** oggetto duplicazione.  
  
 *LockType*  
 Facoltativo. Oggetto [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md) valore che specifica il tipo di blocco dell'originale **Recordset**, o di una sola **Recordset**. I valori validi sono **adLockUnspecified** oppure **adLockReadOnly**.  
  
## <a name="remarks"></a>Note  
 Usare la **Clone** metodo per creare più, Duplica **Recordset** oggetti, soprattutto se si vuole mantenere più di un record corrente in un determinato set di record. Usando il **Clone** è più efficiente rispetto alla creazione e apertura di un nuovo metodo **Recordset** oggetto che usa la stessa definizione dell'originale.  
  
 Il [filtro](../../../ado/reference/ado-api/filter-property.md) proprietà dell'originale **Recordset**, se presente, non verranno applicate per il clone. Impostare il **filtro** proprietà del nuovo **Recordset** per filtrare i risultati. Il modo più semplice per copiare tutte le classi esistenti **filtro** valore consiste nell'assegnarlo direttamente, come indicato di seguito.  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 Il record corrente di un clone appena creato è impostato per il primo record.  
  
 Le modifiche apportate a uno **Recordset** oggetto saranno visibili in tutti i suoi cloni indipendentemente dal tipo di cursore. Tuttavia, dopo l'esecuzione [Requery](../../../ado/reference/ado-api/requery-method.md) sull'originale **Recordset**, non è più cloni verranno sincronizzati con la versione originale.  
  
 Chiusura originale **Recordset** chiusa relative copie, non comporta la chiusura di una copia vicino originale o una delle altre copie.  
  
 È possibile duplicare solo una **Recordset** oggetto che supporta i segnalibri. I valori di segnalibro sono intercambiabili; vale a dire, un riferimento di segnalibro da una **Recordset** oggetto fa riferimento allo stesso record in uno qualsiasi dei suoi cloni.  
  
 Alcuni **Recordset** verificano anche gli eventi che vengono attivati in tutte le **Recordset** cloni. Tuttavia, poiché il record corrente può differire tra clonato **recordset**, gli eventi potrebbero non essere validi per il clone. Ad esempio, se si modifica un valore di un campo, una [WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md) evento verrà generato in modificato **Recordset** e in tutti i cloni. Il *i campi* parametro delle **WillChangeField** eventi di clonato **Recordset** (la modifica non effettuata) farà riferimento ai campi del record corrente del clone, che può essere un record diverso da quello corrente dell'originale **Recordset** in cui si è verificato durante la modifica.  
  
 Nella tabella seguente fornisce un elenco completo di tutte le **Recordset** gli eventi. Indica se sono valida e attivato per i cloni dei recordset generati usando il **Clone** (metodo).  
  
|Evento|Attivazione in cloni?|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|No|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|No|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|No|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Yes|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|No|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Yes|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|Yes|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|Yes|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|No|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|No|  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Clone (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Esempio di metodo Clone (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Esempio di metodo Clone (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
