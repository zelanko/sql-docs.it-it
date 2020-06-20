---
title: Elemento TestServer (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TestServer element
ms.assetid: caa3547a-2cd5-47ad-ace2-a36752835cfe
author: stevestein
ms.author: sstein
ms.openlocfilehash: fe5e58be9d28cc1eae5913e3bfe40eeed6129c3e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007542"
---
# <a name="testserver-element-dta"></a>Elemento TestServer (DTA)
  Indica il server di prova da utilizzare durante l'ottimizzazione di un server di produzione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<TuningOptions>  
  <TestServer>...</TestServer>  
   ...code removed here...  
</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|**string**, lunghezza illimitata.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Facoltativa. È possibile utilizzarlo una volta per ogni elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementi figlio**|No.|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Riduzione del carico di ottimizzazione del server di produzione](../../relational-databases/performance/reduce-the-production-server-tuning-load.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
