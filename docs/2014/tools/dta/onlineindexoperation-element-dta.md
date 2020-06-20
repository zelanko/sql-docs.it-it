---
title: Elemento OnlineIndexOperation (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- OnlineIndexOperation element
ms.assetid: 7c5614cd-09aa-4a59-9591-347aa7d36473
author: stevestein
ms.author: sstein
ms.openlocfilehash: b0911811eb95e1d3dd03e8a4d8e33cd7740277e6
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85040393"
---
# <a name="onlineindexoperation-element-dta"></a>Elemento OnlineIndexOperation (DTA)
  Specifica se è possibile creare online gli indici, le viste indicizzate o le partizioni consigliate da Ottimizzazione guidata motore di database.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <OnlineIndexOperation>...</OnlineIndexOperation>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|`string`, lunghezza illimitata.|  
|**Valori consentiti**|**OFF**<br /> Le strutture di progettazione fisica indicate non possono essere create online.<br /><br /> **ON**<br /> Tutte le strutture di progettazione fisica indicate possono essere create online.<br /><br /> **MIXED**<br /> Ottimizzazione guidata motore di database indica le strutture di progettazione fisica che possono essere create online quando possibile.<br /><br /> Con questo elemento utilizzare solo uno di questi valori. Se si creano indici online, la parola chiave **ONLINE = ON** viene aggiunta alla relativa definizione di oggetto.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Facoltativa. Se utilizzato, può essere utilizzato una sola volta per l'elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementi figlio**|No.|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML semplice &#40;DTA&#41;](simple-xml-input-file-sample-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
