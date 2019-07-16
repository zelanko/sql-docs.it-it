---
title: Metodo DeleteRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 409c4e21395b7b903cf4ff03726fbd37a2a218d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67919080"
---
# <a name="deleterecord-method-ado"></a>Metodo DeleteRecord (ADO)
Elimina un'entità rappresentata da un [Record](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 facoltativo. Oggetto **stringa** valore contenente un URL che identifica l'entità (ad esempio, il file o directory) da eliminare. Se *origine* viene omesso oppure una stringa vuota, l'entità rappresentata dall'oggetto corrente specifica [Record](../../../ado/reference/ado-api/record-object-ado.md) viene eliminato. Se il Record è una raccolta ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) dei **adCollectionRecord**, ad esempio una directory) verranno eliminati anche tutti gli elementi figlio (ad esempio, le sottodirectory).  
  
 *Async*  
 facoltativo. Oggetto **booleana** valore che, quando **True**, specifica che l'operazione di eliminazione è asincrono.  
  
## <a name="remarks"></a>Note  
 Operazioni sull'oggetto rappresentato da questo **Record** potrebbe non riuscire dopo il completamento del metodo. Dopo la chiamata **DeleteRecord**, il **Record** deve essere chiuso perché il comportamento del **Record** può diventare imprevedibile: seconda quando viene aggiornato il provider di **Record** con l'origine dati.  
  
 Se l'oggetto **Record** ottenuto da un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), quindi i risultati di questa operazione non verranno riflessa immediatamente nel **Recordset**. Aggiorna il **Recordset** , chiudere e riaprire lo oppure eseguire il **Recordset** [rieseguire una query](../../../ado/reference/ado-api/requery-method.md) metodo, il [Update](../../../ado/reference/ado-api/update-method.md) metodo, o [Risincronizza](../../../ado/reference/ado-api/resync-method.md) (metodo).  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Delete (raccolta Fields ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Metodo Delete (insieme di parametri ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Metodo Delete (recordset ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
