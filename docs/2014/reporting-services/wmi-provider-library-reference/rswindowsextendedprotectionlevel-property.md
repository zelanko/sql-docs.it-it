---
title: Proprietà RSWindowsExtendedProtectionLevel (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c3c4fdbf8642715a895e8c345ccd171c53ca3509
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63020123"
---
# <a name="rswindowsextendedprotectionlevel-property-wmi-msreportserverconfigurationsetting"></a>Proprietà RSWindowsExtendedProtectionLevel (MSReportServer_ConfigurationSetting WMI)
  Restituisce un valore stringa che indica il livello di protezione supportato dalla configurazione del server di report. Questa proprietà è di sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Note  
 Restituisce un valore stringa che indica il livello di protezione supportato dalla configurazione del server di report. Se il server di report a cui è connesso il provider WMI non supporta la protezione estesa, viene restituita una stringa vuota (""). Nell'elenco seguente sono indicati i valori validi:  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà RSWindowsExtendedProtectionScenario &#40;MSReportServer_ConfigurationSetting WMI&#41;](rswindowsextendedprotectionscenario-property.md)   
 [Metodo SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Protezione estesa per l'autenticazione con Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [File di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
