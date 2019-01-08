---
title: Modello di memorizzazione nella cache (SQLXML 4.0) | Documenti di Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- registry keys [SQLXML]
- cache [SQLXML]
- templates [SQLXML], caching
ms.assetid: 73e151c6-b24e-4422-a116-51e0846bc6f5
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d38459f470bf75d12d9fcd69da96a4d772776c01
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52793713"
---
# <a name="template-caching-sqlxml-40"></a>Memorizzazione nella cache dei modelli (SQLXML 4.0)
  La memorizzazione dei modelli nella cache migliora significativamente le prestazioni. Se è impostata, il modello rimane in memoria fino alla prima esecuzione. In questo modo vengono migliorate le prestazioni per l'esecuzione successiva.  
  
 È possibile impostare le dimensioni della cache dei modelli aggiungendo nel Registro di sistema la chiave seguente:  
  
```  
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\MSSQLServer\Client\SQLXML4\TemplateCacheSize  
```  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoteRegistry](../../../includes/ssnoteregistry-md.md)]  
  
 È consigliabile impostare le dimensioni del modello in base alla memoria disponibile e al numero di modelli utilizzati. Il valore predefinito è **TemplateCacheSize** dimensione è 31. È possibile aumentare le dimensioni della cache se l'accesso al modello sembra lento o ridurle se la memoria è insufficiente.  
  
 Per ottenere prestazioni migliori, si consiglia di impostare **TemplateCacheSize** superiore al numero dei modelli utilizzati normalmente. Se **TemlateCacheSize** è minore rispetto al numero di modelli è, le prestazioni diminuiscono con il numero di aumento di modelli. Il **TemplateCacheSize** può essere impostata su un massimo di 128.  
  
 Ogni volta che viene utilizzato un modello memorizzato nella cache, viene controllata l'ora di modifica del file modello per vedere se deve essere aggiornata. Ciò accade in quanto la copia su disco è più recente della copia della cache.  
  
> [!NOTE]  
>  I parametri di modello e le proprietà dei comandi non vengono memorizzati nella cache.  
  
## <a name="see-also"></a>Vedere anche  
 [La cache dello schema &#40;SQLXML 4.0&#41;](schema-caching-sqlxml-4-0.md)   
 [La memorizzazione nella cache di XSL &#40;SQLXML 4.0&#41;](xsl-caching-sqlxml-4-0.md)  
  
  
