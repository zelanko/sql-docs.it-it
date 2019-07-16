---
title: Metodo MoveRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 157e38c2c9c23ff8f7e92af40385b0962c6dcb70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918069"
---
# <a name="moverecord-method-ado"></a>Metodo MoveRecord (ADO)
Sposta l'entità rappresentata da un [Record](../../../ado/reference/ado-api/record-object-ado.md) in un'altra posizione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativo. Oggetto **stringa** contenente un URL che identifica il **Record** da spostare. Se *origine* viene omesso oppure specifica una stringa vuota, l'oggetto rappresentato da questo **Record** viene spostato. Ad esempio, se il **Record** rappresenta un file, il contenuto del file viene spostati nel percorso specificato da *destinazione*.  
  
 *Destinazione*  
 facoltativo. Oggetto **stringa** contenente un URL che specifica la posizione in cui *origine* verranno spostati.  
  
 *UserName*  
 Facoltativo. Oggetto **stringa** valore contenente l'ID utente, se necessario, autorizza l'accesso al *destinazione*.  
  
 *Password*  
 Facoltativo. Oggetto **stringa** che contiene la password che, se necessario, verifica *UserName*.  
  
 *Opzioni*  
 facoltativo. Oggetto [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) valore il cui valore predefinito è **adMoveUnspecified**. Specifica il comportamento di questo metodo.  
  
 *Async*  
 facoltativo. Oggetto **booleana** valore che, quando **True**, specifica l'operazione deve essere asincrona.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String**. In genere, il valore di *destinazione* viene restituito. Tuttavia, il valore esatto restituito è dipendente dal provider.  
  
## <a name="remarks"></a>Note  
 I valori della *origine* e *destinazione* non deve essere identica; in caso contrario, si verifica un errore di run-time. Almeno i nomi di server, percorso e di risorse devono essere diverso.  
  
 Per i file spostati utilizzando il Provider di pubblicazione Internet, questo metodo aggiorna tutti i collegamenti ipertestuali nel file da spostare a meno che non specificato diversamente dal *opzioni*. Questo metodo ha esito negativo se *destinazione* identifica un oggetto esistente (ad esempio, un file o una directory), a meno che non **adMoveOverWrite** è specificato.  
  
> [!NOTE]
>  Usare la **adMoveOverWrite** opzione con cautela. Se si specifica questa opzione quando si sposta un file in una directory, ad esempio, verrà eliminare la directory e verrà sostituirlo con il file.  
  
 Alcuni attributi delle **Record** dell'oggetto, ad esempio le [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) proprietà, non verrà aggiornato una volta completata questa operazione. Aggiorna il **Record** delle proprietà dell'oggetto chiudendo il **Record**, quindi aprirlo nuovamente con l'URL della posizione in cui è stata spostata il file o directory.  
  
 Se l'oggetto **Record** ottenuto da un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), il nuovo percorso del file spostato o della directory non verrà riflessa immediatamente nel **Recordset**. Aggiorna il **Recordset** chiudendo e aprirlo nuovamente.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious metodi (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (Servizi Desktop remoto)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
