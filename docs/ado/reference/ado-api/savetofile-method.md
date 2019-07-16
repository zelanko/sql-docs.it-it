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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917030"
---
# <a name="savetofile-method"></a>Metodo SaveToFile
Salva il contenuto binario di un [Stream](../../../ado/reference/ado-api/stream-object-ado.md) in un file.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
Stream.SaveToFile FileName, SaveOptions  
```  
  
#### <a name="parameters"></a>Parametri  
 *FileName*  
 Oggetto **stringa** valore contenente il nome completo del file a cui il contenuto del **Stream** verrà salvato. È possibile salvare in un percorso locale valido, o qualsiasi posizione è possibile accedere tramite un valore di tipo UNC.  
  
 *SaveOptions*  
 Oggetto [SaveOptionsEnum](../../../ado/reference/ado-api/saveoptionsenum.md) valore che specifica se deve essere creato un nuovo file da **SaveToFile**, se non esiste già. Valore predefinito è **adSaveCreateNotExists**. Con queste opzioni è possibile specificare che si verifica un errore se il file specificato non esiste. È inoltre possibile specificare che **SaveToFile** sovrascrive il contenuto corrente di un file esistente.  
  
> [!NOTE]
>  Se si sovrascrive un file esistente (quando **adSaveCreateOverwrite** è impostato), **SaveToFile** tronca i byte da un file esistente originale che seguono il nuovo [EOS](../../../ado/reference/ado-api/eos-property.md).  
  
## <a name="remarks"></a>Note  
 **SaveToFile** può essere usato per copiare il contenuto di un **Stream** oggetto in un file locale. Sussiste alcuna modifica nelle proprietà del contenuto o il **Stream** oggetto. Il **Stream** oggetto deve essere aperto prima di chiamare **SaveToFile**.  
  
 Questo metodo non modifica l'associazione del **Stream** oggetto all'origine sottostante. Il **Stream** oggetto continuerà a essere associato con l'URL originale oppure **Record** che è stata la relativa origine all'apertura.  
  
 Dopo una **SaveToFile** operazione, la posizione corrente ([posizione](../../../ado/reference/ado-api/position-property-ado.md)) nel flusso è impostata all'inizio del flusso (0).  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Stream (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Metodo Open (ADO Stream)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Metodo Save](../../../ado/reference/ado-api/save-method.md)
