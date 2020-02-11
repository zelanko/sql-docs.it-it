---
title: Metodo stat | Microsoft Docs
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
ms.openlocfilehash: 0538a3afae1e4c0bf4159d8ef6a42872f21ff6ed
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67916874"
---
# <a name="stat-method"></a>Metodo Stat
Recupera le informazioni su un oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Long stream.Stat(StatStg, StatFlag)  
```  
  
## <a name="return-value"></a>Valore restituito  
 Valore **Long** che indica lo stato dell'operazione.  
  
#### <a name="parameters"></a>Parametri  
 *StatStg*  
 Struttura STATSTG che verrà compilata con le informazioni sul flusso. L'implementazione del metodo **Stat** utilizzato dall'oggetto flusso ADO non compila tutti i campi della struttura.  
  
 *StatFlag*  
 Specifica che questo metodo non restituisce alcuni membri della struttura STATSTG, salvando così un'operazione di allocazione della memoria. I valori vengono ricavati dall'enumerazione STATFLAG. L'enumerazione STATFLAG ha due valori  
  
|Costante|valore|  
|--------------|-----------|  
|STATFLAG_DEFAULT|0|  
|STATFLAG_NONAME|1|  
  
## <a name="remarks"></a>Osservazioni  
 La versione del metodo stat implementato per l'oggetto flusso ADO compila i campi seguenti della struttura STATSTG:  
  
 *pwcsName*  
 Stringa che contiene il nome del flusso, se ne è disponibile uno e il valore StatFlag STATFLAG_NONAME non è stato specificato.  
  
 *cbSize*  
 Specifica la dimensione in byte del flusso o della matrice di byte.  
  
 *mtime*  
 Indica l'ora dell'Ultima modifica di questa archiviazione, flusso o matrice di byte.  
  
 *CTime*  
 Indica l'ora di creazione per questa archiviazione, flusso o matrice di byte.  
  
 *dell'atime*  
 Indica l'ora dell'ultimo accesso per questa archiviazione, flusso o matrice di byte.  
  
 Se STATFLAG_NONAME viene specificato nel parametro StatFlag, il nome del flusso non viene restituito.  
  
 Se STATFLAG_NONAME non è stato specificato nel parametro StatFlag e non è disponibile alcun nome per il flusso corrente, questo valore verrà E_NOTIMPL.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
