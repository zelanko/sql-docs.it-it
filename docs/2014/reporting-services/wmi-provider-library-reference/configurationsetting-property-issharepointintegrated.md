---
title: Proprietà IsSharePointIntegrated (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: c548fed8-5e04-4faf-8b10-b37c86178056
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 08f27657e4ba0e586c5734d2575b5017e8bfc1ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62645915"
---
# <a name="issharepointintegrated-property-wmi"></a>Proprietà IsSharePointIntegrated (WMI)
  Viene specificato se il server di report è in modalità integrata SharePoint. A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], questa proprietà restituisce sempre `False` poiché in modalità SharePoint, le istanze [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] sono servizi condivisi SharePoint e non vengono controllate dai provider WMI.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Oggetto `Boolean` che indica se il server di report è in modalità integrata SharePoint.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
