---
title: Caching di XSL (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- XSL caching [SQLXML]
ms.assetid: 91994142-32f0-4d8d-a8cf-eb0d8b1f1999
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9c23a208a0276a2a3eb71f493aa7e5ce7fad0928
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52749243"
---
# <a name="xsl-caching-sqlxml-40"></a>Memorizzazione nella cache file XSL (SQLXML 4.0)
  La memorizzazione nella cache di fogli di stile XSL migliora le prestazioni. Fino alla prima esecuzione, il foglio di stile XSL resta in memoria se la memorizzazione nella cache XSL è impostata su ON. Questa impostazione offre prestazioni migliori per l'elaborazione successiva. L'impostazione predefinita è ON.  
  
 È possibile impostare le dimensioni della cache per i file XSL aggiungendo la chiave seguente nel Registro di sistema:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\XSLCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 La cache dei file XSL deve essere impostata in base alla memoria disponibile e al numero di fogli di stile XSL utilizzati. Il valore predefinito è **XSLCacheSize** dimensione è 31. È possibile aumentare le dimensioni della cache se l'accesso a XSL appare rallentato oppure diminuire le dimensioni della cache se la memoria risulta insufficiente.  
  
 Per ottenere prestazioni migliori, si consiglia di impostare **XSLCacheSize** superiore al numero di fogli di stile XSL utilizzati normalmente. Se **XSLCacheSize** è minore del numero di XSL fogli di stile si dispone, le prestazioni diminuiscono con il numero di incrementi di fogli di stile XSL. Il **XSLCacheSize** può essere impostata su un massimo di 128.  
  
 Ogni volta che si utilizza il foglio di stile XSL memorizzato nella cache, viene verificata la durata delle modifiche del file XSL per determinare se deve essere aggiornato. Ciò accade in quanto la copia su disco è più recente della copia della cache.  
  
## <a name="see-also"></a>Vedere anche  
 [La cache dei modelli &#40;SQLXML 4.0&#41;](template-caching-sqlxml-4-0.md)   
 [La cache dello schema &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)  
  
  
