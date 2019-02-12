---
title: Metodo InitializeReportServer (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5f6df892b16c7c384291e50640434ce9df15f662
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029222"
---
# <a name="initializereportserver-method-wmi-msreportserverconfigurationsetting"></a>Metodo InitializeReportServer (MSReportServer_ConfigurationSetting WMI)
  Inizializza l'istanza di servizio di report specificata.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parametri  
 *InstallationID*  
 Stringa utilizzata per crittografare la chiave di crittografia prima che venga restituita.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
 *ExtendedErrors[]*  
 [out] Matrice di stringhe che contiene errori aggiuntivi restituiti dalla chiamata.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
 Quando viene chiamato questo metodo, la chiave di crittografia che accede alle informazioni protette del database del server di report viene crittografata tramite la chiave pubblica del server di report identificato da *InstallationID*.  
  
 La chiave pubblica del server di report specificato deve essere stata precedentemente scritta nel database del server di report.  
  
 Il metodo *InitializeReportServer* deve essere chiamato per un server di report che dispone già dell'accesso alle informazioni protette in modo che sia in grado di decrittografare la chiave di crittografia. La chiave di crittografia crittografata risultante viene quindi archiviata nel database del server di report.  
  
 Se il server di report [IsInitialized](configurationsetting-property-isinitialized.md) è impostata su `true` quando viene chiamato il metodo InitializeReportServer, il metodo ha esito positivo senza provare a crittografare la chiave di crittografia.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
