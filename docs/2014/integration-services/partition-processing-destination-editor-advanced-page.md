---
title: Editor destinazione elaborazione partizione (pagina avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.partprocessingtransformation.advanced.f1
helpviewer_keywords:
- Partition Processing Destination Editor
ms.assetid: 2039ee0f-069d-479d-90b2-2a12481b1162
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e3eee8a69013975f7bfe9febcfa85d8143dcef68
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58374900"
---
# <a name="partition-processing-destination-editor-advanced-page"></a>Editor destinazione elaborazione partizione (pagina Avanzate)
  Utilizzare la pagina **Avanzate** della finestra di dialogo **Editor destinazione elaborazione partizione** per configurare la gestione degli errori.  
  
 Per ulteriori informazioni sulla destinazione elaborazione partizione, vedere [Partition Processing Destination](data-flow/partition-processing-destination.md).  
  
> [!NOTE]  
>  Le attività qui descritte non si applicano ai modelli tabulari di Analysis Services.  Non è possibile eseguire il mapping di colonne di input a colonne di partizione per i modelli tabulari. È possibile utilizzare invece l'attività Esegui DDL Analysis Services [Analysis Services Execute DDL Task](control-flow/analysis-services-execute-ddl-task.md) per elaborare la partizione.  
  
## <a name="options"></a>Opzioni  
 **Usa configurazione errori predefinita**  
 Consente di specificare se utilizzare la gestione degli errori predefinita di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Il valore predefinito è `True`.  
  
 **Azione per errore chiave**  
 Consente di specificare la modalità di gestione dei record che hanno valori di chiave non validi.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**ConvertToUnknown**|Consente di convertire il valore di chiave non valido nel valore Sconosciuto.|  
|**DiscardRecord**|Consente di scartare il record.|  
  
 **Ignora errori**  
 Consente di specificare che gli errori devono essere ignorati.  
  
 **Arresta in caso di errore**  
 Consente di specificare che l'elaborazione deve essere arrestata al verificarsi di un errore.  
  
 **Numero di errori**  
 Consente di specificare la soglia di errore alla quale l'elaborazione deve arrestarsi quando è stata selezionata l'opzione **Arresta in caso di errore**.  
  
 **Azione in caso di errore**  
 Consente di specificare l'azione che deve essere intrapresa al raggiungimento della soglia di errore quando è stata selezionata l'opzione **Arresta in caso di errore**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**StopProcessing**|Consente di arrestare l'elaborazione.|  
|**StopLogging**|Consente di arrestare la registrazione degli errori.|  
  
 **Chiave non trovata**  
 Consente di specificare l'azione che deve essere intrapresa per un errore di chiave non trovata. Il valore predefinito è **ReportAndContinue**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave duplicata**  
 Consente di specificare l'azione che deve essere intrapresa per un errore di chiave duplicata. Il valore predefinito è **IgnoreError**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave Null convertita in sconosciuta**  
 Consente di specificare l'azione che deve essere intrapresa quando una chiave Null è stata convertita nel valore Sconosciuto. Il valore predefinito è **IgnoreError**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave Null non consentita**  
 Consente di specificare l'azione che deve essere intrapresa quando viene incontrata una chiave Null e le chiavi Null non sono consentite. Il valore predefinito è **ReportAndContinue**.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Percorso log degli errori**  
 Consente di digitare il percorso del log degli errori o di selezionare una destinazione usando il pulsante Sfoglia **(...)** .  
  
 **Sfoglia (...)**  
 Consente di selezionare il percorso del log degli errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione elaborazione partizione &#40;pagina Mapping&#41;](../../2014/integration-services/partition-processing-destination-editor-mappings-page.md)  
  
  
