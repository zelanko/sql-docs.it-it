---
title: Proprietà AbsolutePage (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePage
helpviewer_keywords:
- AbsolutePage property [ADO]
ms.assetid: ddb58a35-ec3a-423c-a504-3c65e62c23d4
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 12b2e6c6f12fc06cb223551b55cb7f9a38df9ac3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921836"
---
# <a name="absolutepage-property-ado"></a>Proprietà AbsolutePage (ADO)
Indica in quale pagina si trova il record corrente.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Per il codice a 32 bit, imposta o restituisce un valore **Long** compreso tra 1 e il numero di pagine nell'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)) oppure restituisce uno dei valori [PositionEnum](../../../ado/reference/ado-api/positionenum.md) .  
  
 Per il codice a 64 bit, usare un tipo di dati che fornisce l'archiviazione di un valore a 64 bit. Ad esempio, è possibile usare un valore **Long** o un altro valore che può avere una lunghezza di 64 bit, ad esempio DBORDINAL. Non usare i valori **PositionEnum** perché sono limitati alla lunghezza di 32 bit.  
  
## <a name="remarks"></a>Osservazioni  
 Questa proprietà può essere usata per identificare il numero di pagina in cui si trova il record corrente. Usa la proprietà [pageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) per dividere logicamente il numero totale di set di righe dell'oggetto **Recordset** in una serie di pagine, ognuna delle quali ha il numero di record uguale a **pageSize** (ad eccezione dell'ultima pagina, che può avere meno record). Il provider deve supportare la funzionalità appropriata affinché questa proprietà sia disponibile.  
  
-   Quando si recupera o si imposta la proprietà **AbsolutePage** , ADO usa la proprietà [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) e la proprietà [pageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) insieme come indicato di seguito:  
  
-   Per ottenere **AbsolutePage**, ADO recupera prima di tutto il **AbsolutePosition**e quindi lo divide in base alla **pageSize**.  
  
-   Per impostare **AbsolutePage**, ADO sposta il **AbsolutePosition** come segue: moltiplica il valore **pageSize** per il nuovo valore **AbsolutePage** e quindi aggiunge 1 al valore. Di conseguenza, la posizione corrente nel **Recordset** dopo l'impostazione corretta di **AbsolutePage** è il primo record nella pagina.  
  
 Analogamente alla proprietà **AbsolutePosition** , **AbsolutePage** è in base 1 ed è uguale a 1 quando il record corrente è il primo record nel **Recordset**. Impostare questa proprietà per passare al primo record di una pagina specifica. Ottenere il numero totale di pagine dalla proprietà **PageCount** .  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [Esempio di proprietà AbsolutePage, PageCount e PageSize (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [Proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Proprietà PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
