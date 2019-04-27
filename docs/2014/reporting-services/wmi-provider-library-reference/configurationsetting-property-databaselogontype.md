---
title: Proprietà DatabaseLogonType (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- DatabaseLogonType
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DatabaseLogonType property
ms.assetid: 6b592582-4c35-4029-ab86-982fff47d8d6
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: cfe28e2cf9c47f3eebaddbcaa013ad492d715748
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62648986"
---
# <a name="databaselogontype-property-wmi-msreportserverconfigurationsetting"></a>Proprietà DatabaseLogonType (MSReportServer_ConfigurationSetting WMI)
  Specifica se il server di report usa un account del servizio [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, un account utente di Windows o un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per accedere al database del server di report. Di sola lettura.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Dim DatabaseLogonType As Integer  
```  
  
```csharp  
public int DatabaseLogonType;  
```  
  
## <a name="property-values"></a>Valori della proprietà  
 Oggetto `integer` che rappresenta il tipo di accesso.  
  
## <a name="example-code"></a>Codice di esempio  
 [Classe MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="remarks"></a>Note  
 I valori possibili sono:  
  
-   0 per l'account di accesso di Windows  
  
-   1 per l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 per accedere come servizio  
  
 Se si specifica 0 (Windows), è necessario impostare il valore nella proprietà [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) su un account utente di Windows valido corrispondente.  
  
 Se si specifica 1 (SQL Server), accertarsi che il valore di [DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md) corrisponda a un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valido.  
  
 Se si specifica 2 (servizio Windows), il server di report usa un account di [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] e l'account del servizio Windows per accedere al database del server di report. La proprietà DatabaseLogonAccount viene ignorata.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
