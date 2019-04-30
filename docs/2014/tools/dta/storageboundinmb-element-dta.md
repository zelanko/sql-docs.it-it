---
title: Elemento StorageBoundInMB (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 33dbfad3c3774abe3de74d4dbf1d67575630b21e
ms.sourcegitcommit: bd5f23f2f6b9074c317c88fc51567412f08142bb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/24/2019
ms.locfileid: "63460107"
---
# <a name="storageboundinmb-element-dta"></a>Elemento StorageBoundInMB (DTA)
  Specifica lo spazio massimo in megabyte che è possibile riservare all'Ottimizzazione guidata motore di database per le indicazioni di ottimizzazione, ovvero il set di indice e partizionamento.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <StorageBoundInMB>...</ StorageBoundInMB >  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|`unsignedInt`, lunghezza illimitata.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Facoltativo. Può essere utilizzato una sola volta per l'elemento `TuningOptions`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**Elementi figlio**|None|  
  
## <a name="remarks"></a>Note  
 Se si ottimizzano più database, per il calcolo dello spazio vengono considerate le indicazioni per tutti i database. Per impostazione predefinita, nell'Ottimizzazione guidata motore di database vengono utilizzate le dimensioni minori tra gli spazi di archiviazione seguenti:  
  
-   Tre volte le dimensioni dei dati non elaborati correnti nei quali sono incluse le dimensioni totali di heap e indici cluster nelle tabelle.  
  
-   Lo spazio disponibile su tutte le unità disco collegate sommato alle dimensioni dei dati non elaborati.  
  
 Le dimensioni dello spazio di archiviazione predefinite non includono gli indici non cluster e le viste indicizzate.  
  
 Se il valore specificato per l'elemento `StorageBoundInMB` è superiore allo spazio su disco effettivo, verrà restituito un errore ma l'ottimizzazione continuerà. Al termine dell'ottimizzazione, sarà possibile aggiungere spazio su disco per implementare le indicazioni.  
  
## <a name="example"></a>Esempio  
  
## <a name="description"></a>Descrizione  
 Nell'esempio di codice seguente viene illustrata la procedura per impostare un limite di 1500 megabyte per lo spazio massimo su disco utilizzabile da un'indicazione di ottimizzazione:  
  
## <a name="code"></a>Codice  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <StorageBoundInMB>1500</StorageBoundInMB>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
