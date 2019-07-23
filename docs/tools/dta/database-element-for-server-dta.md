---
title: Elemento database per server (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Database element
ms.assetid: 5cd9a87a-af4b-45f3-8c18-f7fd7e7d3064
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5817a6d32ff94aaba7e4c0a573e6cd6a5fd586dc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68116926"
---
# <a name="database-element-for-server-dta"></a>Elemento Database per Server (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
|Occorrenza|Obbligatorio una o più volte in base all'elemento **Server** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|Elemento padre|[Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md)|  
|Elementi figlio|[Elemento Name per Database &#40;DTA&#41;](../../tools/dta/name-element-for-database-dta.md)<br /><br /> [Elemento Schema per Database &#40;DTA&#41;](../../tools/dta/schema-element-for-database-dta.md)|  
  
## <a name="remarks"></a>Remarks  
 Questo elemento appartiene al nome **DatabaseDetailsTypecomplexType** nell'XML Schema di Ottimizzazione guidata motore di database. Questo elemento **Database** non deve essere confuso con quello il cui padre radice è l'elemento **Configuration**. Per altre informazioni, vedere [Elemento Database per Configuration &#40;DTA&#41;](../../tools/dta/database-element-for-configuration-dta.md).  
  
## <a name="example"></a>Esempio  
 Per un esempio di uso di questo elemento **Database** , vedere [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
