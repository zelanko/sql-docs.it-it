---
title: Metodo LoadFromFile (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_LoadFromFile
helpviewer_keywords:
- LoadFromFile method [ADO]
ms.assetid: b18d8d38-7354-4a94-b637-6ac035faa433
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ce90b13a677246fb64462fbe691eb9e3efaa3c7f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67918275"
---
# <a name="loadfromfile-method-ado"></a>Metodo LoadFromFile (ADO)
Carica il contenuto di un file esistente in un [Stream](../../../ado/reference/ado-api/stream-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parametri  
 *FileName*  
 Oggetto **stringa** valore contenente il nome di un file da caricare nella **Stream**. *Nome del file* può contenere qualsiasi percorso valido e il nome in formato UNC. Se il file specificato non esiste, si verifica un errore di run-time.  
  
## <a name="remarks"></a>Note  
 Questo metodo può essere utilizzato per caricare il contenuto di un file locale in un **Stream** oggetto. Ciò consente di caricare il contenuto di un file locale in un server.  
  
 Il **Stream** oggetto deve essere già aperto prima di chiamare **LoadFromFile**. Questo metodo non modifica l'associazione del **Stream** ; dell'oggetto verrà comunque associata all'oggetto specificato dall'URL o **Record** con il quale il **Stream** era in origine aprire.  
  
 **LoadFromFile** sovrascrive il contenuto corrente della **Stream** oggetto con i dati letti dal file. I byte esistenti nel **Stream** vengono sovrascritti dal contenuto del file. I byte rimanenti ed esistenti in precedenza seguendo la [EOS](../../../ado/reference/ado-api/eos-property.md) creando **LoadFromFile**, vengono troncati.  
  
 Dopo una chiamata a **LoadFromFile**, la posizione corrente è impostata all'inizio della **Stream** ([posizione](../../../ado/reference/ado-api/position-property-ado.md) è 0).  
  
 Perché 2 byte possono essere aggiunti all'inizio del flusso per la codifica, le dimensioni del flusso potrebbero non corrispondere esattamente le dimensioni del file da cui è stato caricato.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)
