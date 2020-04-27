---
title: Metodo SaveToFile | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Stream::raw_SaveToFile
- _Stream::SaveToFile
helpviewer_keywords:
- SaveToFile method [ADO]
ms.assetid: 8a8594f2-422b-4d2e-94f8-7fe337445900
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2e56178ad306d5b39c2445c391c3bbabe4fc424
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67917030"
---
# <a name="savetofile-method"></a>Metodo SaveToFile
Salva il contenuto binario di un [flusso](../../../ado/reference/ado-api/stream-object-ado.md) in un file.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parametri  
 *FileName*  
 Valore **stringa** che contiene il nome completo del file in cui verrà salvato il contenuto del **flusso** . È possibile salvare in qualsiasi percorso locale valido o in qualsiasi posizione a cui si ha accesso tramite un valore UNC.  
  
 *SaveOptions*  
 Valore [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) che specifica se un nuovo file deve essere creato da **SaveToFile**, se non esiste già. Il valore predefinito è **adSaveCreateNotExists**. Con queste opzioni è possibile specificare che si verifica un errore se il file specificato non esiste. È anche possibile specificare che **SaveToFile** sovrascrive il contenuto corrente di un file esistente.  
  
> [!NOTE]
>  Se si sovrascrive un file esistente (quando **adSaveCreateOverwrite** è impostato), **SaveToFile** tronca tutti i byte del file esistente originale che seguono la nuova [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Osservazioni  
 **SaveToFile** può essere utilizzato per copiare il contenuto di un oggetto **flusso** in un file locale. Non sono state apportate modifiche al contenuto o alle proprietà dell'oggetto **flusso** . L'oggetto **flusso** deve essere aperto prima di chiamare **SaveToFile**.  
  
 Questo metodo non modifica l'associazione dell'oggetto **flusso** alla relativa origine sottostante. L'oggetto **Stream** sarà comunque associato all'URL o al **record** originale che era l'origine all'apertura.  
  
 Dopo un'operazione **SaveToFile** , la posizione corrente ([position](../../../ado/reference/ado-api/position-property-ado.md)) nel flusso viene impostata all'inizio del flusso (0).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Metodo Open (flusso ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
