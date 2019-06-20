---
title: Metodo SetUnattendedExecutionAccount (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetUnattendedExecutionAccount method
ms.assetid: 1ba6be6f-b05c-4ea0-af98-cd0780290b70
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 095929c60d586fa0ed6c857412a369171acdaa10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66097928"
---
# <a name="setunattendedexecutionaccount-method-wmi-msreportserverconfigurationsetting"></a>Metodo SetUnattendedExecutionAccount (MSReportServer_ConfigurationSetting WMI)
  Specifica l'account utilizzato per l'esecuzione automatica dei report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub SetUnattendedExecutionAccount(UserName as String, _  
    Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetUnattendedExecutionAccount (string UserName,   
    string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *UserName*  
 Account di Windows da utilizzare per le esecuzioni automatiche.  
  
 *Password*  
 Password per l'account specificato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
 Il metodo SetUnattendedExecutionAccount non verifica se il server di report può accedere come utente specificato.  
  
 Non è possibile usare il metodo SetUnattendedExecutionAccount per effettuare esecuzioni automatiche nel contesto del servizio Windows del server di report.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
