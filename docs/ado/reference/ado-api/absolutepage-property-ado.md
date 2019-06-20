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
manager: jroth
ms.openlocfilehash: c87862f97a1fc00d625542c177d85e11d0a7ad45
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66699280"
---
# <a name="absolutepage-property-ado"></a>Proprietà AbsolutePage (ADO)
Indica la pagina in cui risiede il record corrente.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Per il codice a 32 bit, imposta o restituisce un **lungo** valore compreso tra 1 e il numero di pagine nel [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto ([PageCount](../../../ado/reference/ado-api/pagecount-property-ado.md)), o restituisce uno del [PositionEnum ](../../../ado/reference/ado-api/positionenum.md) valori.  
  
 Per il codice a 64 bit, usare un tipo di dati che fornisce per l'archiviazione di un valore a 64 bit. Ad esempio, è possibile usare **lungo** o un altro valore che può essere di lunghezza a 64 bit, ad esempio DBORDINAL. Non utilizzare **PositionEnum** valori perché sono limitate alla lunghezza di 32 bit.  
  
## <a name="remarks"></a>Note  
 Questa proprietà può essere utilizzata per identificare il numero di pagina in cui si trova il record corrente. Usa il [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) proprietà per suddividere logicamente il numero totale di righe delle **Recordset** in una serie di pagine, ognuno dei quali ha il numero di record è uguale all'oggetto **PageSize** (ad eccezione dell'ultima pagina, che può contenere un minor numero di record). Il provider deve supportare le funzionalità appropriate per questa proprietà sia disponibile.  
  
-   Ottenere o impostare il **AbsolutePage** proprietà, utilizza ADO le [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md) proprietà e le [PageSize](../../../ado/reference/ado-api/pagesize-property-ado.md) proprietà insieme come indicato di seguito:  
  
-   Per ottenere il **AbsolutePage**, ADO recuperato prima di tutto il **AbsolutePosition**e si divide per il **PageSize**.  
  
-   Per impostare il **AbsolutePage**, ADO passa il **AbsolutePosition** come indicato di seguito: moltiplica il **PageSize** dalla nuova **AbsolutePage** il valore e quindi aggiunge 1 al valore. Di conseguenza, la posizione corrente di **Recordset** dopo aver impostato correttamente **AbsolutePage** rappresenta il primo record in tale pagina.  
  
 Ad esempio la **AbsolutePosition** proprietà, **AbsolutePage** è basata su 1 ed è uguale a 1 quando il record corrente è il primo record nel **Recordset**. Impostare questa proprietà per spostare il primo record di una pagina particolare. Ottenere il numero totale di pagine dal **PageCount** proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [AbsolutePage, PageCount, PageSize esempio di proprietà e (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize esempio di proprietà e (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [Proprietà AbsolutePosition (ADO)](../../../ado/reference/ado-api/absoluteposition-property-ado.md)   
 [Proprietà PageCount (ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)   
 [Proprietà PageSize (ADO)](../../../ado/reference/ado-api/pagesize-property-ado.md)
