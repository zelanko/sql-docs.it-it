---
title: Elemento database per Configuration (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: e91ba243-6cc9-457a-8f5a-134f3c71ae69
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fbca62a5d32ed6b7ec30eb5d6dba6a82a2b80c64
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747283"
---
# <a name="database-element-for-configuration-dta"></a>Elemento Database per Configuration (DTA)
  Specifica il database sul quale l'Ottimizzazione guidata motore di database eseguirà la valutazione della configurazione ipotetica indicata dall'elemento `Configuration`.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuna.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Obbligatorio una o più volte per elemento `Server`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Server per Configuration &#40;DTA&#41;](server-element-for-configuration-dta.md)|  
|**Elementi figlio**|[Elemento Name per Database &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento Schema per Database &#40;DTA&#41;](schema-element-for-database-dta.md)<br /><br /> [Elemento Recommendation &#40;DTA&#41;](recommendation-element-dta.md)|  
  
## <a name="remarks"></a>Note  
 Questo elemento appartiene al nome **DatabaseTypecomplexType** nell'XML Schema di Ottimizzazione guidata motore di database. Questo elemento `Database` non deve essere confuso con l'elemento il cui padre di livello radice è l'elemento `Server` presente all'inizio del file di input XML. Per altre informazioni, vedere [Elemento Database per Server &#40;DTA&#41;](database-element-for-server-dta.md).  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo `Database` elemento, vedere la [esempio di File di Input XML con configurazione specificata dall'utente &#40;DTA&#41;](xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
