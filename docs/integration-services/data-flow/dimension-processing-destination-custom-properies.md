---
description: Proprietà personalizzate della destinazione elaborazione dimensione
title: Proprietà personalizzate della destinazione elaborazione dimensione | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9700f663-53f2-49b6-b1ef-92c7b752d6a1
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e6959edde524e2219573793b5becb34f5d63f1c
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192723"
---
# <a name="dimension-processing-destination-custom-properies"></a>Proprietà personalizzate della destinazione elaborazione dimensione

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  La destinazione elaborazione dimensione include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione elaborazione dimensione. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ASConnectionString|string|Stringa di connessione a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|KeyDuplicate|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, valore che indica come gestire gli errori di chiave duplicata. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **IgnoreError** (0).|  
|KeyErrorAction|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica come gestire gli errori di chiave. I valori possibili sono **ConvertToUnknown** (0) e **DiscardRecord** (1). Il valore predefinito della proprietà è **ConvertToUnknown** (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration è **False**, il limite massimo consentito di errori di chiave.|  
|KeyErrorLimitAction|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica l'azione da eseguire quando viene raggiunto il **KeyErrorLimit** . I valori possibili sono **StopLogging** (1) e **StopProcessing** (0). Il valore predefinito di questa proprietà è **StopProcessing** (0).|  
|KeyErrorLogFile|string|Quando UseDefaultConfiguration è **False**, il percorso e il nome del file di log degli errori.|  
|KeyNotFound|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica come gestire gli errori di chiave mancanti. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **IgnoreError** (0).|  
|NullKeyConvertedToUnknown|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica come gestire le chiavi Null convertite a un valore sconosciuto. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **IgnoreError** (0).|  
|NullKeyNotAllowed|Integer (enumerazione)|Quando UseDefaultConfiguration è **False**, un valore che indica come gestire i valori Null non consentiti. I valori possibili sono **IgnoreError** (0), **ReportAndContinue** (1) e **ReportAndStop** (2). Il valore predefinito di questa proprietà è **IgnoreError** (0).|  
|ProcessType|Integer (enumerazione)|Tipo di elaborazione della dimensione utilizzata dalla trasformazione. I valori sono **ProcessAdd** (1) (incrementale), **ProcessFull** (0), e **ProcessUpdate** (2).|  
|UseDefaultConfiguration|Boolean|Valore che specifica se la trasformazione utilizza la configurazione degli errori predefinita. Se questa proprietà è **False**, la trasformazione include informazioni sull'elaborazione degli errori.|  
  
 L'input e le colonne di input della destinazione elaborazione dimensione non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione elaborazione dimensione](../../integration-services/data-flow/dimension-processing-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](./set-the-properties-of-a-data-flow-component.md)  
  
