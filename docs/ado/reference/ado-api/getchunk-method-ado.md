---
title: Metodo GetChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::raw_GetChunk
- Field20::GetChunk
helpviewer_keywords:
- GetChunk method [ADO]
ms.assetid: fc268e22-205b-44a3-9038-ffed51e23e10
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: c5dc09043d780c2a743059773eed56e16a799bf5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694946"
---
# <a name="getchunk-method-ado"></a>Metodo GetChunk (ADO)
Restituisce tutte le o in parte, il contenuto di un testo di grandi dimensioni o dati binari [campo](../../../ado/reference/ado-api/field-object.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
variable = field.GetChunk(Size)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **Variant**.  
  
#### <a name="parameters"></a>Parametri  
 *Dimensione*  
 Oggetto **lungo** espressione che è uguale al numero di byte o caratteri che si desidera recuperare.  
  
## <a name="remarks"></a>Note  
 Usare la **GetChunk** metodo su un **campo** oggetto per recuperare la parte o tutti i relativi dati caratteri o binari long. In situazioni in cui la memoria di sistema è limitata, è possibile usare la **GetChunk** metodo per modificare i valori long in parti, anziché nella loro interezza.  
  
 I dati che un **GetChunk** chiamata restituisce viene assegnato a *variabile*. Se *dimensioni* è maggiore rispetto ai dati rimanenti, il **GetChunk** metodo restituisce solo i dati rimanenti senza spaziatura interna *variabile* con gli spazi vuoti. Se il campo è vuoto, il **GetChunk** metodo restituisce un valore null.  
  
 Ogni successivo **GetChunk** chiamata recupera i dati a partire dalla posizione in cui il precedente **GetChunk** chiamata è stata interrotta. Tuttavia, se si recuperano dati da un campo e quindi impostare o leggere il valore di un altro campo nel record corrente, ADO presuppone che sia stata completata il recupero dei dati dal primo campo. Se si chiama il **GetChunk** metodo nel primo campo anche in questo caso, ADO interpreta la chiamata come nuovo **GetChunk** operazione e inizia la lettura dall'inizio dei dati. L'accesso ai campi in altre [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetti che non sono i cloni dei primi **Recordset** oggetto non interromperà **GetChunk** operazioni.  
  
 Se il **adFldLong** bit nel [attributi](../../../ado/reference/ado-api/attributes-property-ado.md) proprietà di un **campo** è impostata su **True**, è possibile usare il **GetChunk**  metodo per il campo.  
  
 Se non è presente nessun record corrente quando si usa la **GetChunk** metodo su un **campo** dell'oggetto, verrà generato errore 3021 (Nessun record corrente).  
  
> [!NOTE]
>  Il **GetChunk** metodo non opera sui **campo** gli oggetti di un [Record](../../../ado/reference/ado-api/record-object-ado.md) oggetto. Esegue alcuna operazione e produrrà un errore di run-time.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di AppendChunk e GetChunk (esempio di metodi (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Esempio di AppendChunk e GetChunk esempio di metodi (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Metodo AppendChunk (ADO)](../../../ado/reference/ado-api/appendchunk-method-ado.md)   
 [Proprietà attributi (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)
