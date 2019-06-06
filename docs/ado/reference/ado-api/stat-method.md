---
title: Metodo Stat | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::Stat
helpviewer_keywords:
- Stat method [ADO]
ms.assetid: 99a2b2d4-e6b1-4205-b011-72d024ea7240
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5f19d1b9ef0dc3b200a895d05728f6985544203b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66719074"
---
# <a name="stat-method"></a>Metodo Stat
Recupera le informazioni su un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Oggetto **lungo** valore che indica lo stato dell'operazione.  
  
#### <a name="parameters"></a>Parametri  
 *StatStg*  
 Struttura STATSTG che verrà compilata con informazioni sul flusso. L'implementazione del **Stat** metodo utilizzata dall'oggetto Stream ADO non inserire tutti i campi della struttura.  
  
 *StatFlag*  
 Specifica che questo metodo non restituisce alcuni dei membri nella struttura STATSTG, risparmiando un'operazione di allocazione di memoria. I valori sono ricavati dall'enumerazione STATFLAG. L'enumerazione STATFLAG presenta due valori  
  
|Costante|Value|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Note  
 La versione del metodo Stat implementata per l'oggetto Stream ADO vengono compilati i seguenti campi della struttura STATSTG:  
  
 *pwcsName*  
 Stringa contenente il nome del flusso, se disponibile e il valore StatFlag non è stata specificata.  
  
 *cbSize*  
 Specifica la dimensione in byte del flusso o matrice di byte.  
  
 *mtime*  
 Indica l'ora dell'ultima modifica per questo archivio, flusso o matrice di byte.  
  
 *ctime*  
 Indica l'ora di creazione per questa archiviazione, flusso o matrice di byte.  
  
 *atime*  
 Indica l'ora dell'ultimo accesso per questo archivio, flusso o matrice di byte.  
  
 Se viene specificato nel parametro StatFlag, non viene restituito il nome del flusso.  
  
 Se non viene specificato nel parametro StatFlag e nessun nome è disponibile per il flusso corrente, questo valore sarà E_NOTIMPL.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
