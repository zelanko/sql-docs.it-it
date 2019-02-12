---
title: Proprietà DatabaseLogonTimeout (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonTimeout Property
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonTimeout property
ms.assetid: 4a65162c-33de-485e-8fd3-2bd6bff8bf8d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: ef5793aa278d9d1a1b9a10f45a68dd5a97442f69
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56019132"
---
# <a name="databaselogontimeout-property-wmi-msreportserverconfigurationsetting"></a>Proprietà DatabaseLogonTimeout (MSReportServer_ConfigurationSetting WMI)
  Specifica il numero di secondi di attesa prima che un tentativo di accesso al database del server di report abbia esito negativo. Il valore **0** indica un tempo di attesa indefinito. Sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim DatabaseLogonTimeout As Int32  
```  
  
```csharp  
public Int32 DatabaseLogonTimeout;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Oggetto integer a 32 bit con segno che rappresenta il numero di secondi.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
