---
title: Elemento Table per schema (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Table element [DTA]
ms.assetid: a59e8319-05d1-47f3-af39-7d970ab8e7dc
author: stevestein
ms.author: sstein
ms.openlocfilehash: 622b5a02f0b13e9cbf6a78977a07daea93a3f520
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85007583"
---
# <a name="table-element-for-schema-dta"></a>Elemento Table per Schema (DTA)
  Specifica la tabella per l'ottimizzazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Schema>  
...code removed here...  
    <Table>...</Table>  
```  
  
## <a name="element-attributes"></a>Attributi elemento  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`NumberOfRows`|Facoltativa. Valore intero che consente la simulazione di tabelle di diverse dimensioni.|  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|**string**, tra 1 e 255 caratteri.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Facoltativa. Elenca tutte le tabelle appropriate per il carico di lavoro.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Schema per Database &#40;DTA&#41;](schema-element-for-database-dta.md)|  
|**Elementi figlio**|[Elemento Name per Table &#40;DTA&#41;](name-element-for-table-dta.md)|  
  
## <a name="remarks"></a>Osservazioni  
 Se non si specifica un elemento `Table`, l'Ottimizzazione guidata motore di database considererà ottimizzabili tutte le tabelle contenute nel database specificato.  
  
## <a name="example"></a>Esempio  
 Per un esempio d'uso, vedere [Elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
