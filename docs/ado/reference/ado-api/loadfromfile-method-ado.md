---
description: Metodo LoadFromFile (ADO)
title: Metodo LoadFromFile (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 76c00998c8fd7c3c6f737ab9b2ab0e2e35c74101
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88990702"
---
# <a name="loadfromfile-method-ado"></a>Metodo LoadFromFile (ADO)
Carica il contenuto di un file esistente in un [flusso](./stream-object-ado.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.LoadFromFileFileName  
```  
  
#### <a name="parameters"></a>Parametri  
 *FileName*  
 Valore **stringa** che contiene il nome di un file da caricare nel **flusso**. *Filename* può contenere qualsiasi percorso e nome valido in formato UNC. Se il file specificato non esiste, si verificherà un errore di run-time.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo può essere utilizzato per caricare il contenuto di un file locale in un oggetto **flusso** . Questa operazione può essere utilizzata per caricare il contenuto di un file locale in un server.  
  
 Prima di chiamare **LoadFromFile**, è necessario che l'oggetto **flusso** sia già aperto. Questo metodo non modifica l'associazione dell'oggetto **flusso** . verrà comunque associato all'oggetto specificato dall'URL o al **record** con cui è stato originariamente aperto il **flusso** .  
  
 **LoadFromFile** sovrascrive il contenuto corrente dell'oggetto **flusso** con i dati letti dal file. Tutti i byte esistenti nel **flusso** vengono sovrascritti dal contenuto del file. Tutti i byte precedentemente esistenti e rimanenti che seguono l' [EOS](./eos-property.md) creata da **LoadFromFile**vengono troncati.  
  
 Dopo una chiamata a **LoadFromFile**, la posizione corrente viene impostata sull'inizio del **flusso** ([position](./position-property-ado.md) è 0).  
  
 Poiché è possibile aggiungere 2 byte all'inizio del flusso per la codifica, la dimensione del flusso potrebbe non corrispondere esattamente alle dimensioni del file da cui è stato caricato.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](./stream-object-ado.md)