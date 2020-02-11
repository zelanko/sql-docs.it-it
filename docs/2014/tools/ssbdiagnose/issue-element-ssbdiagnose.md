---
title: Elemento Issue (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 69b9e356fcaf4b5abd97b56c69ecdd9881aaaee2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63285764"
---
# <a name="issue-element-ssbdiagnose"></a>Elemento Issue (ssbdiagnose)
  Segnala un problema rilevato dall'utilità **ssbdiagnose** . Nel file di output XML di **ssbdiagnose** è presente un solo elemento Issue per ogni problema segnalato.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>Attributi elemento  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`type`|Identifica la categoria del problema segnalato dall'elemento Issue:<br /><br /> **"Diagnosi"** Segnala un problema di configurazione rilevato quando si analizza [!INCLUDE[ssSB](../../includes/sssb-md.md)] una configurazione di.<br /><br /> **"Problema"** Segnala un problema che ha impedito a **ssbdiagnose** di completare l'analisi. Correggere il problema ed eseguire di nuovo **ssbdiagnose**.<br /><br /> **"Evento"** Segnala un [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] evento rilevato quando si esegue un controllo **-Runtime** . Gli eventi vengono segnalati solo se è specificata l'opzione **-SHOWEVENTS** .|  
|`code`|Identifica il numero di errore relativo al messaggio.|  
|`server`|Identifica l'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] in cui è stato rilevato il problema. Se il problema si è verificato in un'istanza predefinita, l'attributo server è costituito solo del nome del computer, mentre se il problema si è verificato in un'istanza denominata, il formato dell'attributo server è NomeComputer\NomeIstanza.|  
|`database`|Identifica il nome dell'istanza del database in cui è stato rilevato il problema.|  
|`object`|Identifica il nome dell'istanza dell'oggetto in cui è stato rilevato il problema. Se il problema si è verificato a livello di istanza o di database, l'attributo dell'oggetto ripete il nome dell'istanza o del database.|  
  
## <a name="element-characteristics"></a>Caratteristiche elemento  
  
|Caratteristica|Descrizione|  
|--------------------|-----------------|  
|**Tipo di dati e lunghezza**|
  `string`, lunghezza illimitata.|  
|**Valore**|Restituisce il testo del messaggio di errore.|  
|**Occorrenza**|Una volta per ogni errore segnalato.|  
  
## <a name="element-relationships"></a>Relazioni elemento  
  
|Relazione|Elementi|  
|------------------|--------------|  
|**Elemento padre**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementi figlio**|nessuno|  
  
## <a name="example"></a>Esempio  
 Questo elemento segnala un errore 1102 per un database che non dispone di una chiave master, in cui l'errore è stato rilevato quando è stata analizzata una configurazione di [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Utilità ssbdiagnose &#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
