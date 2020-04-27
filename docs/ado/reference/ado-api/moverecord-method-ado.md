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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918069"
---
# <a name="moverecord-method-ado"></a>Metodo MoveRecord (ADO)
Sposta l'entità rappresentata da un [record](../../../ado/reference/ado-api/record-object-ado.md) in un'altra posizione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parametri  
 *origine*  
 Facoltativo. Valore **stringa** che contiene un URL che identifica il **record** da spostare. Se *source* viene omesso o specifica una stringa vuota, l'oggetto rappresentato da questo **record** viene spostato. Se, ad esempio, il **record** rappresenta un file, il contenuto del file viene spostato nel percorso specificato da *destinazione*.  
  
 *Destination*  
 Facoltativo. Valore **stringa** che contiene un URL che specifica la posizione in cui verrà spostato l'oggetto di *origine* .  
  
 *Nome utente*  
 Facoltativo. Valore **stringa** che contiene l'ID utente che, se necessario, autorizza l'accesso alla *destinazione*.  
  
 *Password*  
 Facoltativo. **Stringa** che contiene la password che, se necessario, verifica il *nome utente*.  
  
 *Opzioni*  
 Facoltativo. Valore [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) il cui valore predefinito è **adMoveUnspecified**. Specifica il comportamento di questo metodo.  
  
 *Async*  
 Facoltativo. Valore **booleano** che, se impostato su **true**, specifica che questa operazione deve essere asincrona.  
  
## <a name="return-value"></a>Valore restituito  
 Valore **String**. In genere, viene restituito il valore di *Destination* . Tuttavia, il valore esatto restituito è dipendente dal provider.  
  
## <a name="remarks"></a>Osservazioni  
 I valori di *source* e *Destination* non devono essere identici. in caso contrario, si verificherà un errore di run-time. Almeno il server, il percorso e i nomi delle risorse devono essere diversi.  
  
 Per i file spostati utilizzando il provider di pubblicazione Internet, questo metodo aggiorna tutti i collegamenti ipertestuali nei file spostati se non diversamente specificato dalle *Opzioni*. Questo metodo ha esito negativo se la *destinazione* identifica un oggetto esistente (ad esempio, un file o una directory), a meno che non sia specificato **adMoveOverWrite** .  
  
> [!NOTE]
>  Usare l'opzione **adMoveOverWrite** in giudizio. Se ad esempio si specifica questa opzione quando si trasferisce un file in una directory, la directory verrà eliminata e sostituita con il file.  
  
 Alcuni attributi dell'oggetto **record** , ad esempio la proprietà [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) , non verranno aggiornati al termine dell'operazione. Aggiornare le proprietà dell'oggetto **record** chiudendo il **record**, quindi riaprendolo con l'URL della posizione in cui il file o la directory è stata spostata.  
  
 Se questo **record** è stato ottenuto da un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), la nuova posizione del file o della directory spostata non verrà riflessa immediatamente nel **Recordset**. Per aggiornare il **Recordset** , chiuderlo e riaprirlo.  
  
> [!NOTE]
>  Gli URL che usano lo schema http richiameranno automaticamente il [provider di Microsoft OLE DB per la pubblicazione Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per ulteriori informazioni, vedere [URL assoluto e relativo](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Metodo Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [Metodi MoveFirst, MoveLast, MoveNext e MovePrevious (Servizi Desktop remoto)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
