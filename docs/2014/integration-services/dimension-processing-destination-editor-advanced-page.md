---
title: Editor destinazione elaborazione dimensione (pagina Avanzate) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.dimprocessingtransformation.advanced.f1
helpviewer_keywords:
- Dimension Processing Destination Editor
ms.assetid: 2b30835a-2680-4d98-89a4-4f17e29e3818
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 5bef21b424c401d77b9d8f3477de4061c3ff0f3d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966959"
---
# <a name="dimension-processing-destination-editor-advanced-page"></a>Editor destinazione elaborazione dimensione (pagina Avanzate)
  Usare la pagina **Avanzate** della finestra di dialogo **Editor destinazione elaborazione dimensione** per configurare la gestione degli errori.  
  
 Per ulteriori informazioni sulla destinazione elaborazione dimensione, vedere [Dimension Processing Destination](data-flow/dimension-processing-destination.md).  
  
## <a name="options"></a>Opzioni  
 **Usare la configurazione degli errori predefinita.**  
 Consente di specificare se utilizzare la gestione degli errori predefinita di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Per impostazione predefinita, questo valore è `True`.  
  
 **Azione per errore chiave**  
 Consente di specificare la modalità di gestione dei record che hanno valori di chiave non validi.  
  
|valore|Description|  
|-----------|-----------------|  
|**ConvertToUnknown**|Consente di convertire il valore di chiave non valido nel valore `UnknownMember`.|  
|**DiscardRecord**|Consente di scartare il record.|  
  
 **Ignora errori**  
 Consente di specificare che gli errori devono essere ignorati.  
  
 **Arresta in caso di errore**  
 Consente di specificare che l'elaborazione deve essere arrestata al verificarsi di un errore.  
  
 **Numero di errori**  
 Consente di specificare la soglia di errore alla quale l'elaborazione deve arrestarsi quando è stata selezionata l'opzione **Arresta in caso di errore**.  
  
 **Azione in caso di errore**  
 Consente di specificare l'azione che deve essere intrapresa al raggiungimento della soglia di errore quando è stata selezionata l'opzione **Arresta in caso di errore**.  
  
|valore|Description|  
|-----------|-----------------|  
|**StopProcessing**|Consente di arrestare l'elaborazione.|  
|**StopLogging**|Consente di arrestare la registrazione degli errori.|  
  
 **Chiave non trovata**  
 Consente di specificare l'azione che deve essere intrapresa per un errore di chiave non trovata. Il valore predefinito è **ReportAndContinue**.  
  
|valore|Description|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave duplicata**  
 Consente di specificare l'azione che deve essere intrapresa per un errore di chiave duplicata. Il valore predefinito è **IgnoreError**.  
  
|valore|Description|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave Null convertita in sconosciuta**  
 Consente di specificare l'azione che deve essere intrapresa quando una chiave Null è stata convertita nel valore `UnknownMember`. Il valore predefinito è **IgnoreError**.  
  
|valore|Description|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Chiave Null non consentita**  
 Consente di specificare l'azione che deve essere intrapresa quando viene incontrata una chiave Null e le chiavi Null non sono consentite. Il valore predefinito è **ReportAndContinue**.  
  
|valore|Description|  
|-----------|-----------------|  
|**IgnoreError**|Consente di ignorare l'errore e continuare l'elaborazione.|  
|**ReportAndContinue**|Consente di segnalare l'errore e continuare l'elaborazione.|  
|**ReportAndStop**|Consente di segnalare l'errore e arrestare l'elaborazione.|  
  
 **Percorso log degli errori**  
 Consente di digitare il percorso del log degli errori o di selezionare una destinazione con il pulsante **Sfoglia (...)**.  
  
 **Sfoglia (...)**  
 Consente di selezionare il percorso del log degli errori.  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione elaborazione dimensione &#40;pagina Gestione connessione&#41;](../../2014/integration-services/dimension-processing-destination-editor-connection-manager-page.md)   
 [Editor destinazione elaborazione dimensione &#40;pagina Mapping&#41;](../../2014/integration-services/dimension-processing-destination-editor-mappings-page.md)  
  
  
