---
title: Elemento StorageBoundInMB (DTA) | Microsoft Docs
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
- StorageBoundInMB element
ms.assetid: a8374910-bf68-4edb-b464-53a3a705e7f4
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 42c0949add779848e7681eee3b70a2122728c71b
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/10/2019
ms.locfileid: "67733452"
---
# <a name="storageboundinmb-element-dta"></a>Elemento StorageBoundInMB (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
|**Tipo di dati e lunghezza**|**unsignedInt**, lunghezza illimitata.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Facoltativo. Può essere utilizzato una sola volta per l'elemento **TuningOptions** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento TuningOptions &#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**Elementi figlio**|None|  
  
## <a name="remarks"></a>Remarks  
 Se si ottimizzano più database, per il calcolo dello spazio vengono considerate le indicazioni per tutti i database. Per impostazione predefinita, nell'Ottimizzazione guidata motore di database vengono utilizzate le dimensioni minori tra gli spazi di archiviazione seguenti:  
  
-   Tre volte le dimensioni dei dati non elaborati correnti nei quali sono incluse le dimensioni totali di heap e indici cluster nelle tabelle.  
  
-   Lo spazio disponibile su tutte le unità disco collegate sommato alle dimensioni dei dati non elaborati.  
  
 Le dimensioni dello spazio di archiviazione predefinite non includono gli indici non cluster e le viste indicizzate.  
  
 Se il valore specificato per l'elemento **StorageBoundInMB** è superiore allo spazio su disco effettivo, verrà restituito un errore ma l'ottimizzazione continuerà. Al termine dell'ottimizzazione, sarà possibile aggiungere spazio su disco per implementare le indicazioni.  
  
## <a name="example"></a>Esempio  
  
## <a name="description"></a>Descrizione  
 Nell'esempio di codice seguente viene illustrata la procedura per impostare un limite di 1500 megabyte per lo spazio massimo su disco utilizzabile da un'indicazione di ottimizzazione:  
  
## <a name="code"></a>codice  
  
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
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
