---
title: Proprietà DatabaseLogonAccount (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonAccount
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonAccount property
ms.assetid: 55f2863f-1ac1-4519-b512-e7f11c0ea5ea
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: c9192e0845a5a6df9c7b848a3f91368dd15cfc60
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56025062"
---
# <a name="databaselogonaccount-property-wmi-msreportserverconfigurationsetting"></a>Proprietà DatabaseLogonAccount (MSReportServer_ConfigurationSetting WMI)
  Specifica l'account di accesso utilizzato dal server di report al momento della connessione al database del server di report. Sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim DatabaseLogonAccount As String  
```  
  
```csharp  
public string DatabaseLogonAccount;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Oggetto `String` che rappresenta il nome dell'account di accesso.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Note  
 I valori validi per questa proprietà varieranno a seconda del valore della proprietà [DatabaseLogonType](configurationsetting-property-databaselogontype.md) .  
  
 Questa proprietà viene ignorata se il [DatabaseLogonType](configurationsetting-property-databaselogontype.md) è impostata su `2 (Service)`.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
