---
title: Comando TAG DELETE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE TAG command [ODBC]
ms.assetid: 4f4e1362-a5f3-4b15-8a3c-d4e96605f221
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eabecbc399751f03e9e5c25b32423ce0839072dc
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53207750"
---
# <a name="delete-tag-command"></a>DELETE TAG (comando)
Rimuove un tag o i tag da un file di indice composto (cdx).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argomenti  
 *TagName1*OF *CDXFileName1*[, *TagName2*[OF *CDXFileName2*]]...  
 Specifica un tag da rimuovere da un file di indice composto. È possibile eliminare più tag con un TAG DELETE includendo un elenco di nomi di tag separati da virgole. Se due o più tag con lo stesso nome esiste nel file di indice aperta, è possibile rimuovere un tag da un file di indice specifico includendo OF *CDXFileName*.  
  
 Tutti i [OF *CDXFileName*]  
 Rimuove tutti i tag da un file di indice composto. Se la tabella corrente include un file di indice composto strutturale, tutti i tag vengono rimossi dal file di indice, il file di indice viene eliminato dal disco e il flag nell'intestazione della tabella che indica la presenza di un file di indice composto strutturale associato viene rimosso. Utilizzare ALL con OF *CDXFileName* per rimuovere tutti i tag da un file di indice composto open diverso dal file di indice composto strutturale.  
  
## <a name="remarks"></a>Note  
 File di indice composto, creati con indice, contengono tag corrispondenti alle voci di indice. Elimina TAG viene usato per rimuovere un tag o i tag dai file di indice composto aperta. È possibile eliminare solo i tag dal file di indice composto aperti nell'area di lavoro corrente. Se si rimuovono tutti i tag da un file di indice composto, il file viene eliminato dal disco.  
  
 Visual FoxPro cerca prima di un tag nel file di indice composto strutturale (se è aperta). Se il tag non è nel file di indice composto strutturale, Visual FoxPro cerca quindi il tag in altri file di indice composto aperta.  
  
## <a name="see-also"></a>Vedere anche  
 [INDEX (comando)](../../odbc/microsoft/index-command.md)
