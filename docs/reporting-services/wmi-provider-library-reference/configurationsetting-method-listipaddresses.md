---
description: Metodo ListIPAddresses (MSReportServer_ConfigurationSetting WMI)
title: Metodo ListIPAddresses (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListIPAddresses method
ms.assetid: 7e7cf182-fba0-4604-a474-098461e23e9d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 822b2022bd8a6ede5c750c1560f1e1424e9576ad
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480633"
---
# <a name="configurationsetting-method---listipaddresses"></a>Metodo di ConfigurationSetting - ListIPAddresses
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
  
 *Lunghezza*  
 [out] Lunghezza della matrice restituita dal metodo.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Osservazioni  
 Le stringhe*IPVersion* sono V4, V6.  
  
 Se *IsDhcpEnabled* è **True**, *IPAddress* è dinamico. Non deve essere usato per le associazioni TLS.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
