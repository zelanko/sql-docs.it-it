---
title: Elemento DatabaseToConnect (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- DatabaseToConnect element
ms.assetid: 65153a66-3aee-4429-99b7-0816ac23c285
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fef2df598d96b33def41f27345f88226fd4c6b5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63185419"
---
# <a name="databasetoconnect-element-dta"></a>Elemento DatabaseToConnect (DTA)
  Specifica il primo database al quale Ottimizzazione guidata motore di database si connette durante l'ottimizzazione di un carico di lavoro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
    <TuningOptions>  
...code removed here...  
      <DatabaseToConnect>...</DatabaseToConnect>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|`string`, lunghezza illimitata.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Facoltativo. È possibile utilizzarlo una volta per ogni elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementi figlio**|None|  
  
## <a name="remarks"></a>Note  
 Utilizzare `DatabaseToConnect` per specificare il nome del primo database al quale si desidera che Ottimizzazione guidata motore di database si connetta quando viene avviata la sessione di ottimizzazione. È possibile specificare un solo database con questo elemento. Se vengono specificati più nomi di database, Ottimizzazione guidata motore di database restituisce un errore.  
  
## <a name="example"></a>Esempio  
 Per un esempio di uso, vedere [Esempio di file di input XML con carico di lavoro inline &#40;DTA&#41;](xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
