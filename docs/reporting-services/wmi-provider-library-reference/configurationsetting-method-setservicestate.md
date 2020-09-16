---
description: Metodo SetServiceState (MSReportServer_ConfigurationSetting WMI)
title: Metodo SetServiceState (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 3607488ec4a9511c9cf95410a4c249a740132d82
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480603"
---
# <a name="configurationsetting-method---setservicestate"></a>Metodo di ConfigurationSetting - SetServiceState
  Attiva e disattiva i servizi Windows ReportServer e Web ReportServer.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *EnableWindowsService*  
 Valore **booleano** che indica lo stato del servizio Windows. Un valore **true** avvia il servizio Windows ReportServer; un valore **false** arresta il servizio Windows.  
  
 *EnableWebService*  
 Valore **booleano** che indica lo stato del servizio Web [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Un valore **true** avvia il servizio Windows ReportServer; un valore **false** arresta il servizio Web  
  
 *EnableReportManager*  
 Valore **booleano** che indica lo stato desiderato per Gestione report.
 
 > [!NOTE] 
 > Questa impostazione è stata deprecata a partire dall'aggiornamento cumulativo 2 di SQL Server 2016 Reporting Services. Il portale Web verrà sempre abilitato. Il valore verrà ignorato.
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
