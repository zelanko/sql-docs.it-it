---
title: Proprietà RSWindowsExtendedProtectionScenario (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 60a61ca96aafe0e475d28023276c561f49c13cde
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66096976"
---
# <a name="rswindowsextendedprotectionscenario-property-wmi-msreportserverconfigurationsetting"></a>Proprietà RSWindowsExtendedProtectionScenario (MSReportServer_ConfigurationSetting WMI)
  Restituisce un valore stringa che indica lo scenario di protezione estesa consentito dalla configurazione del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## <a name="remarks"></a>Note  
 Restituisce un valore stringa che indica lo scenario di protezione estesa consentito dalla configurazione del server di report. Se il server di report a cui è connesso il provider WMI non supporta la protezione estesa, viene restituita una stringa vuota ("").  
  
 Nell'elenco seguente sono indicati i valori validi:  
  
 `"Any | Proxy | Direct"`  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà RSWindowsExtendedProtectionLevel &#40;MSReportServer_ConfigurationSetting WMI&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Metodo SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Protezione estesa per l'autenticazione con Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [File di configurazione RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
