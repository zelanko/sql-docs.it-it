---
title: Elemento TuningOptions (DTA) | Microsoft Docs
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
- TuningOptions element
ms.assetid: 58a22ba1-8e03-411f-bd46-85e4540f217a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 20b266aa90f9c1a68607468e284fe9e5d8eb9e95
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105922"
---
# <a name="tuningoptions-element-dta"></a>Elemento TuningOptions (DTA)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Contiene le opzioni di ottimizzazione per una specifica sessione di ottimizzazione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions>  
```  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuna.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Facoltativo. Se utilizzato, può essere utilizzato una sola volta per ogni elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementi figlio**|Elemento**ReportSet** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**TuningLogTable** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**NumberOfEvents** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> [Elemento TuningTimeInMin &#40;DTA&#41;](../../tools/dta/tuningtimeinmin-element-dta.md)<br /><br /> [Elemento StorageBoundInMB &#40;DTA&#41;](../../tools/dta/storageboundinmb-element-dta.md)<br /><br /> Elemento**MaxKeyColumnsInIndex** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**MaxColumnsInIndex** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**MinPercentageImprovement** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100)<br /><br /> [Elemento TestServer &#40;DTA&#41;](../../tools/dta/testserver-element-dta.md)<br /><br /> [Elemento FeatureSet &#40;DTA&#41;](../../tools/dta/featureset-element-dta.md)<br /><br /> [Elemento Partitioning &#40;DTA&#41;](../../tools/dta/partitioning-element-dta.md)<br /><br /> [Elemento DropOnlyMode &#40;DTA&#41;](../../tools/dta/droponlymode-element-dta.md)<br /><br /> [Elemento KeepExisting &#40;DTA&#41;](../../tools/dta/keepexisting-element-dta.md)<br /><br /> [Elemento OnlineIndexOperation &#40;DTA&#41;](../../tools/dta/onlineindexoperation-element-dta.md)<br /><br /> [Elemento DatabaseToConnect &#40;DTA&#41;](../../tools/dta/databasetoconnect-element-dta.md)<br /><br /> Elemento**IgnoreConstantsInWorkload** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).<br /><br /> Elemento**RetainShellDB** . Per ulteriori informazioni, vedere l' [XML Schema di Ottimizzazione guidata motore di database](https://go.microsoft.com/fwlink/?linkid=43100).|  
  
## <a name="example"></a>Esempio  
 Per alcuni esempi di elemento **TuningOptions**, vedere [Esempi di file di input XML &#40; DTA &#41;](../../tools/dta/xml-input-file-samples-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
