---
title: Elemento database per Server (DTA) | Microsoft Docs
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
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9b23e8d7f68cca0722691863a2c5c8d5e095c33c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62661833"
---
# <a name="database-element-for-server-dta"></a>Elemento Database per Server (DTA)
  Specifica il database che si desidera ottimizzare in uno specifico server.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Server>  
...code removed here...  
    <Database>...</Database>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|Tipo di dati e lunghezza|Nessuna.|  
|Valore predefinito|Nessuno|  
|Occorrenza|Obbligatorio una o più volte per elemento `Server`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|Elemento padre|[Elemento Server &#40;DTA&#41;](server-element-dta.md)|  
|Elementi figlio|[Elemento Name per Database &#40;DTA&#41;](name-element-for-database-dta.md)<br /><br /> [Elemento Schema per Database &#40;DTA&#41;](schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Note  
 Questo elemento appartiene al nome **DatabaseDetailsTypecomplexType** nell'XML Schema di Ottimizzazione guidata motore di database. Questo elemento `Database` non deve essere confuso con quello il cui padre radice è l'elemento `Configuration`. Per altre informazioni, vedere [Elemento Database per Configuration &#40;DTA&#41;](database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di `Database` elemento, vedere [elemento Server &#40;DTA&#41;](server-element-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
