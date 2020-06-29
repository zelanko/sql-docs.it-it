---
title: Proprietà personalizzate della destinazione elaborazione partizione | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 3eac4413-0c90-4b06-8f7e-d0d72f4d869d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 04d5f9a669fbccc798698914c919e63d90e04591
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431598"
---
# <a name="partition-processing-destination-custom-properties"></a>Proprietà personalizzate della destinazione elaborazione partizione
  La destinazione elaborazione partizione include sia proprietà personalizzate che le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della destinazione elaborazione partizione. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ASConnectionString|string|Stringa di connessione a un progetto [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].|  
|KeyDuplicate|Integer (enumerazione)|Quando UseDefaultConfiguration è `False` , valore che indica come gestire gli errori di chiave duplicata. I valori possibili sono `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). Il valore predefinito di questa proprietà è `IgnoreError` (0).|  
|KeyErrorAction|Integer (enumerazione)|Quando UseDefaultConfiguration è `False` , valore che indica come gestire gli errori di chiave. I valori possibili sono `ConvertToUnknown` (0) e `DiscardRecord` (1). Il valore predefinito di questa proprietà è `ConvertToUnknown` (0).|  
|KeyErrorLimit|Integer|Quando UseDefaultConfiguration è `False` , il limite superiore degli errori di chiave consentiti.|  
|KeyErrorLimitAction|Integer (enumerazione)|Quando UseDefaultConfiguration è `False` , valore che indica l'azione da eseguire quando `KeyErrorLimit` viene raggiunto. I valori possibili sono `StopLogging` (1) e `StopProcessing` (0). Il valore predefinito di questa proprietà è `StopProcessing` (0).|  
|KeyErrorLogFile|string|Quando UseDefaultConfiguration è `False` , il percorso e il nome del file di log degli errori.|  
|KeyNotFound|Integer (enumerazione)|Quando UseDefaultConfiguration è `False` , valore che indica come gestire gli errori di chiave mancanti. I valori possibili sono `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). Il valore predefinito di questa proprietà è `ReportAndContinue` (1).|  
|NullKeyConvertedToUnknown|Integer (enumerazione)|Quando UseDefaultConfiguration è `False` , valore che indica come gestire le chiavi null convertite nel valore sconosciuto. I valori possibili sono `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). Il valore predefinito di questa proprietà è `IgnoreError` (0).|  
|NullKeyNotAllowed|Integer (enumerazione)|Quando UseDefaultConfiguration è `False` , valore che indica come gestire i valori null non consentiti. I valori possibili sono `IgnoreError` (0), `ReportAndContinue` (1) e `ReportAndStop` (2). Il valore predefinito di questa proprietà è `ReportAndContinue` (1).|  
|ProcessType|Integer (enumerazione)|Tipo di elaborazione della partizione utilizzata dalla trasformazione. I valori possibili sono `ProcessAdd` (1) (incrementale), `ProcessFull` (0) e `ProcessUpdate` (2).|  
|UseDefaultConfiguration|Boolean|Valore che specifica se la trasformazione utilizza la configurazione degli errori predefinita. Se questa proprietà è `False` , la trasformazione utilizza i valori delle proprietà personalizzate di gestione degli errori elencate in questa tabella, inclusi duplicati, KeyErrorAction e così via.|  
  
 L'input e le colonne di input della destinazione elaborazione partizione non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Destinazione elaborazione partizione](partition-processing-destination.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà comuni](../common-properties.md)  
  
  
