---
title: Proprietà SecureConnectionLevel (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SecureConnectionLevel
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b461114bdab4ae982356f550bb1cf146b3a3d762
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62646059"
---
# <a name="secureconnectionlevel-property-wmi-msreportserverconfigurationsetting"></a>Proprietà SecureConnectionLevel (MSReportServer_ConfigurationSetting WMI)
  Restituisce il livello di connessione protetta specificato nel file RSReportServer.config. Di sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Valore `Integer` che rappresenta il livello di connessione protetto. I valori restituiti indicano se SSL è o non è configurato. Il valore maggiore di o pari a 1 indica che SSL è abilitato. Il valore 0 indica che SSL è disattivato.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
