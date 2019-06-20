---
title: Metodo SetWindowsServiceIdentity (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d08e9900453fe259d727e202489d728e0dce47e0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097880"
---
# <a name="setwindowsserviceidentity-method-wmi-msreportserverconfigurationsetting"></a>Metodo SetWindowsServiceIdentity (MSReportServer_ConfigurationSetting WMI)
  Consente l'esecuzione del servizio Windows ReportServer in base a un utente di Windows specificato e concede a tale account autorizzazioni per il file system sufficienti, in modo da consentire il funzionamento del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub SetWindowsServiceIdentity(UseBuiltInAccount as Boolean, _  
    Account as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetWindowsServiceIdentity(boolean UseBuiltInAccount,   
    string Account, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *UseBuiltInAccount*  
 Indica se l'account specificato è un account predefinito di Windows.  
  
 *Account*  
 Account di Windows da utilizzare per eseguire il servizio Windows, nel formato "DOMAIN\alias."  
  
 *Password*  
 Password per l'account.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
 Quando il *UseBuiltInAccount* parametro è impostato su `true` e il server di report è in esecuzione in Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] o Windows XP, il valore della *Name*, *dominio*, e *Password* i parametri vengono ignorati e viene usato l'account sistema locale.  
  
 Quando la *UseBuiltInAccount* parametro è impostato su `true` e il server di report è in esecuzione in Windows Server 2003, il *dominio* e *Password* sono di proprietà ignorato, e il campo del nome deve contenere "Builtin\system" o "Builtin\System" o "Builtin\LocalService".  
  
 Il metodo SetWindowsServiceIdentity imposta le autorizzazioni per i file su file e cartelle nella directory di installazione del server di report.  
  
 L'account specificato nella *Account* parametro richiede `LogonAsService` diritti in Windows. Il metodo concede questo diritto all'account specificato.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
