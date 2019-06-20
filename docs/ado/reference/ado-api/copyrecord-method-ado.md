---
title: Metodo CopyRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d11a8d5d775499246bd8af709764dec3f2ad61e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698514"
---
# <a name="copyrecord-method-ado"></a>Metodo CopyRecord (ADO)
Copia di un'entità rappresentata da un [record](../../../ado/reference/ado-api/record-object-ado.md) in un'altra posizione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parametri  
 *Origine*  
 Facoltativo. Oggetto **stringa** valore contenente un URL che specifica l'entità deve essere copiato (ad esempio, un file o directory). Se *origine* viene omesso oppure specifica una stringa vuota, il file o directory rappresentata dall'oggetto corrente [Record](../../../ado/reference/ado-api/record-object-ado.md) verranno copiati.  
  
 *Destinazione*  
 Facoltativo. Oggetto **stringa** contenente un URL che specifica la posizione in cui *origine* verranno copiati.  
  
 *UserName*  
 Facoltativo. Oggetto **stringa** valore contenente l'ID utente, se necessario, autorizza l'accesso al *destinazione*.  
  
 *Password*  
 Facoltativo. Oggetto **stringa** valore contenente la password, se necessario, verifica *UserName*.  
  
 *Opzioni*  
 Facoltativo. Oggetto [CopyRecordOptionsEnum uguale al](../../../ado/reference/ado-api/copyrecordoptionsenum.md) valore con valore predefinito è **adCopyUnspecified**. Specifica il comportamento di questo metodo.  
  
 *Async*  
 Facoltativo. Oggetto **booleana** valore che, quando **True**, specifica che questa operazione deve essere asincrona.  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **stringa** valore che restituisce in genere il valore di *destinazione*. Tuttavia, il valore esatto restituito è dipendente dal provider.  
  
## <a name="remarks"></a>Note  
 I valori della *origine* e *destinazione* non deve essere identica; in caso contrario, si verifica un errore di run-time. Almeno uno dei nomi di server, percorso o risorsa deve essere diverso.  
  
 Tutti gli elementi figlio (ad esempio, le sottodirectory) del *origine* vengono copiati in modo ricorsivo, a meno che non **adCopyNonRecursive** è specificato. In un'operazione ricorsiva *destinazione* non deve essere una sottodirectory della *origine*; in caso contrario, l'operazione non verrà completata.  
  
 Questo metodo ha esito negativo se *destinazione* identifica un'entità esistente (ad esempio, un file o una directory), a meno che non **adCopyOverWrite** è specificato.  
  
> [!IMPORTANT]
>  Usare la **adCopyOverWrite** opzione con cautela. Ad esempio, se si specifica questa opzione quando si copia un file in una directory verrà *eliminare* la directory e sostituirlo con il file.  
  
> [!NOTE]
>  Gli URL che utilizzano lo schema http chiama automaticamente il [Provider Microsoft OLE DB per Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Per altre informazioni, vedere [URL assoluti e relativi](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
