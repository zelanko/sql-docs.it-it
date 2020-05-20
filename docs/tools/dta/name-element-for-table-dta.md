---
title: Elemento Name per Table (DTA)
description: Nell'utilità dta l'elemento Name per Table specifica un nome di tabella per l'ottimizzazione. Questo articolo descrive tale elemento.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Name element
ms.assetid: 422a755f-ee52-4863-b1aa-f4ef1b8fd0bb
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: cb397cf7642f4b523c0919ac70c06f6a3442ef46
ms.sourcegitcommit: b8933ce09d0e631d1183a84d2c2ad3dfd0602180
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/13/2020
ms.locfileid: "83151860"
---
# <a name="name-element-for-table-dta"></a>Elemento Name per Table (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
|**Tipo di dati e lunghezza**|**string**, tra 1 e 255 caratteri.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Obbligatorio. Una volta per ogni elemento **Table** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento Table per Schema &#40;DTA&#41;](../../tools/dta/table-element-for-schema-dta.md)|  
|**Elementi figlio**|No.|  
  
## <a name="example"></a>Esempio  
 Per un esempio d'uso, vedere [Elemento Server &#40;DTA&#41;](../../tools/dta/server-element-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
