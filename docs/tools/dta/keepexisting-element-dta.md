---
title: Elemento KeepExisting (DTA) | Microsoft Docs
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
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fafd931dd05726285ee505f1d68ca59d28c0c59d
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727639"
---
# <a name="keepexisting-element-dta"></a>Elemento KeepExisting (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Specifica le strutture di progettazione fisica (indici, viste indicizzate o partizionamento) che Ottimizzazione guidata motore di database deve mantenere quando genera l'indicazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <KeepExisting>...</KeepExisting>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|**string**, limite della lunghezza imposto dal server.|  
|**Valori consentiti**|**NONE**<br /> Nessuna struttura esistente.<br /><br /> **ALL**<br /> Tutte le strutture esistenti.<br /><br /> **ALIGNED**<br /> Tutte le strutture con partizionamento allineato.<br /><br /> **CL_IDX**<br /> Tutti gli indici cluster nelle tabelle.<br /><br /> **IDX**<br /> Tutti gli indici cluster e non cluster nelle tabelle.<br /><br /> Utilizzare solo uno dei valori seguenti con questo elemento.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Facoltativo. È possibile usarla una volta per ogni elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementi figlio**|Nessuna.|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML semplice &#40;DTA&#41;](../../tools/dta/simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
