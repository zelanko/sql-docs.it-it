---
title: Elemento KeepExisting (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- KeepExisting element
ms.assetid: e67aae61-d06d-4a03-85ba-6516c3502dce
author: stevestein
ms.author: sstein
ms.openlocfilehash: bcfa71becfda386031d6267e2b7f97f1eac5b731
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048347"
---
# <a name="keepexisting-element-dta"></a>Elemento KeepExisting (DTA)
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
|**Tipo di dati e lunghezza**|`string`, limite della lunghezza imposto dal server.|  
|**Valori consentiti**|**NONE**<br /> Nessuna struttura esistente.<br /><br /> **ALL**<br /> Tutte le strutture esistenti.<br /><br /> **ALIGNED**<br /> Tutte le strutture con partizionamento allineato.<br /><br /> **CL_IDX**<br /> Tutti gli indici cluster nelle tabelle.<br /><br /> **IDX**<br /> Tutti gli indici cluster e non cluster nelle tabelle.<br /><br /> Utilizzare solo uno dei valori seguenti con questo elemento.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Facoltativa. Può essere utilizzato una sola volta per ogni elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementi figlio**|No.|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML semplice &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
