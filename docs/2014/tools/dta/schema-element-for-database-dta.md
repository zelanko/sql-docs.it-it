---
title: Elemento schema per Database (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Schema element
ms.assetid: d932e59c-953f-4ab4-934d-b6baf344835c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 74e72deb65d3f693e309926870174ebe72817c3e
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52769403"
---
# <a name="schema-element-for-database-dta"></a>Elemento Schema per Database (DTA)
  Specifica lo schema del database che si desidera ottimizzare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Database>  
...code removed here...  
    <Schema>...</Schema>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuna.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Obbligatorio una sola volta per l'elemento **Database** specificato nell'elemento **Server** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Database per Server &#40;DTA&#41;](database-element-for-server-dta.md)|  
|**Elementi figlio**|[Elemento Name per Schema &#40;DTA&#41;](name-element-for-schema-dta.md)<br /><br /> [Elemento Table per Schema &#40;DTA&#41;](table-element-for-schema-dta.md)|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
