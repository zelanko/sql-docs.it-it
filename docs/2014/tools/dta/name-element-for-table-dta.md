---
title: Elemento Name per Table (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 422a755f-ee52-4863-b1aa-f4ef1b8fd0bb
author: stevestein
ms.author: sstein
ms.openlocfilehash: cdaf7cc0e4e96f7e58c80a074df636f603d89a6f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040384"
---
# <a name="name-element-for-table-dta"></a>Elemento Name per Table (DTA)
  Specifica il nome di una tabella da ottimizzare.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Schema>  
    <Table>  
        <Name>...</Name>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|`string`, tra 1 e 255 caratteri.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Obbligatorio. Una volta per ogni elemento `Table`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Table per Schema &#40;DTA&#41;](table-element-for-schema-dta.md)|  
|**Elementi figlio**|No.|  
  
## <a name="example"></a>Esempio  
 Per un esempio d'uso, vedere [Elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
