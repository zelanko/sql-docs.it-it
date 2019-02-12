---
title: Metodo ListIPAddresses (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 1c6854194122dbc4ab5e1781ea62de119f7a09e9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56029052"
---
# <a name="listipaddresses-method-wmi-msreportserverconfigurationsetting"></a>Metodo ListIPAddresses (MSReportServer_ConfigurationSetting WMI)
  Elenca gli indirizzi IP per il computer del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub ListIPAddresses (ByRef IPAddress() as String, _  
    ByRef IPVersion()as String, ByRef IsDhcpEnabled () as Boolean, _   
    ByRef Length as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListIPAddresses (out string[] IPAddress,   
    out string[] IPVersion, out bool[] isDhcpEnabled, out int length,   
    out int HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *IPAddress[]*  
 [out] Elenco degli indirizzi IP per il computer.  
  
 *IPVersion[]*  
 [out] Versione degli indirizzi IP.  
  
 *IsDhcpEnabled[]*  
 [out] Indica se gli indirizzi IP sono abilitati a DHCP.  
  
 *Length*  
 [out] Lunghezza della matrice restituita dal metodo.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Note  
 Le stringhe*IPVersion* sono V4, V6.  
  
 Se *IsDhcpEnabled* viene `True`, il *IPAddress* è dinamico. Non deve essere utilizzato per le associazioni SSL.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
