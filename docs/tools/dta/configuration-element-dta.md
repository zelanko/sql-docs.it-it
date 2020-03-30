---
title: Elemento Configuration (DTA)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 79073bca20afa853c1b6fbf548ed804f71f074fe
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307980"
---
# <a name="configuration-element-dta"></a>Elemento Configuration (DTA)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Definisce una configurazione specificata dall'utente costituita da strutture di progettazione fisica esistenti e ipotetiche da analizzare in Ottimizzazione guidata motore di database durante l'ottimizzazione di un carico di lavoro.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<DTAInput>  
    <Server>...</Server>  
    <Workload>...</Workload>  
    <TuningOptions>...</TuningOptions  
    <Configuration [SpecificationMode="Relative" | "Absolute"]>  
    ...code removed here...  
    </Configuration>  
</DTAInput>  
```  
  
## <a name="element-attributes"></a>Attributi elemento  
  
|Attributo di configurazione|Descrizione|  
|-----------------------------|-----------------|  
|**SpecificationMode**|Facoltativa. Indica se Ottimizzazione guidata motore di database deve analizzare la configurazione specificata in relazione alla configurazione esistente corrente o come configurazione autonoma completamente nuova. Usare un tipo di dati **string** per specificare questo attributo con uno dei valori consentiti seguenti:<br /><br /> **Relative**:<br />                  Valuta la configurazione specificata in relazione alla configurazione esistente corrente delle strutture di progettazione fisica (indici, viste indicizzate, partizionamento) nel database sottoposto a ottimizzazione. Ad esempio:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Valuta la configurazione specificata come configurazione autonoma. Se viene specificato Absolute, Ottimizzazione guidata motore di database non prende in considerazione la configurazione esistente. Ad esempio:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|No.|  
|**Valore predefinito**|No.|  
|**Occorrenza**|Facoltativa. Consentito una sola volta per ogni elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementi figlio**|[Elemento Server per Configuration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
