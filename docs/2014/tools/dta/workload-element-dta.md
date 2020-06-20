---
title: Elemento Workload (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: stevestein
ms.author: sstein
ms.openlocfilehash: f409e978bf977d48fbfc3a9ec56d5ebfe2b545ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064086"
---
# <a name="workload-element-dta"></a>Elemento Workload (DTA)
  Specifica il carico di lavoro da utilizzare per una sessione di ottimizzazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|No.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Obbligatorio una sola volta per ogni elemento `DTAInput`.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Avviare e usare Ottimizzazione guidata motore di database](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**Elementi figlio**|[Elemento File &#40;DTA&#41;](file-element-dta.md)<br /><br /> [Elemento Database per Workload &#40;DTA&#41;](database-element-for-workload-dta.md)<br /><br /> [Elemento EventString &#40;DTA&#41;](eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Osservazioni  
 Un carico di lavoro è un set di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] eseguite sui database che si desidera ottimizzare. Ottimizzazione guidata motore di database può utilizzare come carichi di lavoro script [!INCLUDE[tsql](../../includes/tsql-md.md)] , file di traccia e tabelle di traccia.  
  
 Se viene specificato un carico di lavoro in un file di input XML e un carico di lavoro nella riga di comando con lo strumento **dta** , per l'ottimizzazione verrà utilizzato il carico di lavoro specificato nella riga di comando. Tutte le opzioni di ottimizzazione specificate nella riga di comando prevalgono su quelle specificate in un file di input XML. L'unica eccezione è rappresentata dal caso in cui una configurazione definita dall'utente venga specificata in modalità di valutazione nel file di input XML. Se, ad esempio, viene immessa una configurazione nell'elemento `Configuration` del file di input XML e anche l'elemento `EvaluateConfiguration` viene specificato come una delle opzioni di ottimizzazione, le opzioni di ottimizzazione specificate nel file di input XML prevarranno su qualsiasi opzione di ottimizzazione immessa dalla riga di comando.  
  
 È necessario specificare un carico di lavoro per ogni sessione di ottimizzazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente viene specificata la tabella di traccia **database. MyDBOwner. TuningTable001** per l' `Workload` elemento. La tabella **TuningTable001** è stata creata con il modello Tuning di SQL Server Profiler e salvando l'output della traccia come tabella.  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
