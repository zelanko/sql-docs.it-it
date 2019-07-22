---
title: Elemento Configuration (DTA) | Microsoft Docs
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
- Configuration element
ms.assetid: 1478e56f-57c4-4441-bac9-1ac91453839b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 767bc5c9d84d8ee0ee14bb74a5b5722604ee9f93
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949822"
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
|**SpecificationMode**|Facoltativo. Indica se Ottimizzazione guidata motore di database deve analizzare la configurazione specificata in relazione alla configurazione esistente corrente o come configurazione autonoma completamente nuova. Usare un tipo di dati **string** per specificare questo attributo con uno dei valori consentiti seguenti:<br /><br /> **Relative**:<br />                  Valuta la configurazione specificata in relazione alla configurazione esistente corrente delle strutture di progettazione fisica (indici, viste indicizzate, partizionamento) nel database sottoposto a ottimizzazione. Esempio:<br /><br /> `<Configuration SpecificationMode="Relative">`<br /><br /> **Absolute**:<br />                  Valuta la configurazione specificata come configurazione autonoma. Se viene specificato Absolute, Ottimizzazione guidata motore di database non prende in considerazione la configurazione esistente. Esempio:<br /><br /> `<Configuration SpecificationMode="Absolute">`|  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|Nessuna.|  
|**Valore predefinito**|Nessuna.|  
|**Occorrenza**|Facoltativo. Consentito una sola volta per ogni elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento DTAInput &#40;DTA&#41;](../../tools/dta/dtainput-element-dta.md)|  
|**Elementi figlio**|[Elemento Server per Configuration &#40;DTA&#41;](../../tools/dta/server-element-for-configuration-dta.md)|  
  
## <a name="example"></a>Esempio  
 Per un esempio di utilizzo di questo elemento, vedere [Esempio di file di input XML con configurazione specificata dall'utente &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-user-specified-configuration-dta.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai file di input XML&#40; (Ottimizzazione guidata motore di database)&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
