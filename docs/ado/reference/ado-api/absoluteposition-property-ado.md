---
title: Proprietà AbsolutePosition (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AbsolutePosition
helpviewer_keywords:
- AbsolutePosition property [ADO]
ms.assetid: 79f8ee5e-fc70-46d8-8c29-ebf943c66592
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4444c54df6e3629e7f69e3fe0d54625f66c3e703
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63155177"
---
# <a name="absoluteposition-property-ado"></a>Proprietà AbsolutePosition (ADO)
Indica la posizione ordinale di una [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) record corrente dell'oggetto.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Per il codice a 32 bit, imposta o restituisce un **lungo** valore compreso tra 1 e il numero di record nelle **Recordset** oggetto ([RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)), o restituisce uno del [ PositionEnum](../../../ado/reference/ado-api/positionenum.md) valori.  
  
 Per il codice a 64 bit, usare un tipo di dati che fornisce per l'archiviazione di un valore a 64 bit. Ad esempio, si potrebbe usare prolungata o un altro valore che rappresenta la lunghezza a 64 bit, ad esempio DBORDINAL. Non utilizzare **PositionEnum** valori poiché sono limitate alla lunghezza di 32 bit.  
  
## <a name="remarks"></a>Note  
 Per impostare il **esempio di AbsolutePosition** proprietà, ADO richiede che implementino il provider OLE DB si usa la [IRowsetLocate:IRowset](https://msdn.microsoft.com/library/windows/desktop/ms721190.aspx) interfaccia.  
  
 L'accesso di **esempio di AbsolutePosition** proprietà di un **Recordset** che è stato aperto con un tipo forward-only o cursore dinamico viene generato l'errore **adErrFeatureNotAvailable**. Gli altri tipi di cursore, verrà restituita nella posizione corretta, purché il provider OLE DB supporta il **IRowsetScroll:IRowsetLocate** interfaccia. Se il provider non supporta il **IRowsetScroll** interfaccia, la proprietà è impostata su **adPosUnknown**. Vedere la documentazione relativa al provider per determinare se supporta **IRowsetScroll**.  
  
 Usare la **esempio di AbsolutePosition** la posizione ordinale in base alle proprietà per passare a un record il **Recordset** oggetto, o per determinare la posizione ordinale del record corrente. Il provider deve supportare le funzionalità appropriate per questa proprietà sia disponibile.  
  
 Ad esempio la [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) proprietà, **AbsolutePosition** è basata su 1 ed è uguale a 1 quando il record corrente è il primo record nel **Recordset**. È possibile ottenere il numero totale di record nel **Recordset** dell'oggetto dalle [RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md) proprietà.  
  
 Quando si impostano i **esempio di AbsolutePosition** proprietà, anche se è in un record di cache corrente, ADO consente di ricaricare la cache con un nuovo gruppo di record che iniziano con il record è specificati. Il [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) proprietà determina la dimensione di questo gruppo.  
  
> [!NOTE]
>  È consigliabile non usare la **esempio di AbsolutePosition** proprietà come un numero di record di surrogati. La posizione di un determinato record viene modificato quando si elimina un record precedente. Non vi è alcuna garanzia che un determinato record avrà lo stesso **esempio di AbsolutePosition** se il **Recordset** oggetto viene rieseguito o riaperto. I segnalibri sono ancora lo strumento consigliato per mantenere e restituire dati in una posizione specificata e sono l'unico modo il posizionamento in tutti i tipi di **Recordset** oggetti.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di AbsolutePosition e CursorLocation (esempio di proprietà (VB)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vb.md)   
 [Esempio di AbsolutePosition e CursorLocation in proprietà XML (VC + +)](../../../ado/reference/ado-api/absoluteposition-and-cursorlocation-properties-example-vc.md)   
 [Proprietà AbsolutePage (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [Proprietà RecordCount (ADO)](../../../ado/reference/ado-api/recordcount-property-ado.md)
