---
title: Metodo SetWindowsServiceIdentity (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetWindowsServiceIdentity (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetWindowsServiceIdentity method
ms.assetid: 9bbc734c-9e69-48c2-8bec-8abe7c6cc987
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b12b21fe8e51f8c03bf01efd7df63053c528781
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "65570916"
---
# <a name="configurationsetting-method---setwindowsserviceidentity"></a>Metodo di ConfigurationSetting - SetWindowsServiceIdentity
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
  
## <a name="remarks"></a>Osservazioni  
 Quando il parametro *UseBuiltInAccount* è impostato su **true** e il server di report è in esecuzione in Microsoft [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)] o Windows XP, il valore dei parametri *Nome*, *Dominio*e *Password* vengono ignorati e si usa l'account di sistema locale.  
  
 Quando il parametro *UseBuiltInAccount* è impostato su **true** e il server di report è in esecuzione in Windows Server 2003, le proprietà *Dominio* e *Password* vengono ignorate e il campo del nome deve contenere "Builtin\NetworkService", "Builtin\System" o "Builtin\LocalService".  
  
 Il metodo SetWindowsServiceIdentity imposta le autorizzazioni per i file su file e cartelle nella directory di installazione del server di report.  
  
 L'account specificato nel parametro *Account* richiede diritti **LogonAsService** in Windows. Il metodo concede questo diritto all'account specificato.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
