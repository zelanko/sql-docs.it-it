---
title: Comando DELETE TAG Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97ca5abca7e70f5dffdae9bf14ce64429fd203d5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303542"
---
# <a name="delete-tag-command"></a>DELETE TAG (comando)
Rimuove uno o più tag da un file di indice composto (con estensione cdx).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
DELETE TAG TagName1 [OF CDXFileName1]  
   [, TagName2 [OF CDXFileName2]] ...  
  Or   
DELETE TAG ALL [OF CDXFileName]  
```  
  
## <a name="arguments"></a>Argomenti  
 *Nome tag1* OF *CDXFileName1*[, *NomeTag2*[DI *CDXFileName2*]] ...  
 Specifica un tag da rimuovere da un file di indice composto. È possibile eliminare più tag con un TAG DELETE includendo un elenco di nomi di tag separati da virgole. Se nei file di indice aperti sono presenti due o più tag con lo stesso nome, è possibile rimuovere un tag da un file di indice specifico includendo *CDXFileName*.  
  
 ALL [OF *CDXFileName*]  
 Rimuove ogni tag da un file di indice composto. Se la tabella corrente dispone di un file di indice composto strutturale, tutti i tag vengono rimossi dal file di indice, il file di indice viene eliminato dal disco e il flag nell'intestazione della tabella indica la presenza di un file di indice composto strutturale associato viene rimosso. Utilizzare ALL with OF *CDXFileName* per rimuovere tutti i tag da un file di indice composto aperto diverso dal file di indice composto strutturale.  
  
## <a name="remarks"></a>Osservazioni  
 I file di indice composti, creati con INDEX, contengono tag corrispondenti alle voci di indice analitico. DELETE TAG viene utilizzato per rimuovere uno o più tag dai file di indice composto aperti. È possibile eliminare solo i tag dai file di indice composto aperti nell'area di lavoro corrente. Se si rimuovono tutti i tag da un file di indice composto, il file viene eliminato dal disco.  
  
 Visual FoxPro cerca innanzitutto un tag nel file di indice composto strutturale (se presente). Se il tag non si trova nel file di indice composto strutturale, Visual FoxPro cerca il tag negli altri file di indice composto aperto.  
  
## <a name="see-also"></a>Vedere anche  
 [INDEX (comando)](../../odbc/microsoft/index-command.md)
