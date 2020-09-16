---
description: Metodo ListReservedURLs (MSReportServer_ConfigurationSetting WMI)
title: Metodo ListReservedURLs (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- ListReservedURLs method
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e19d6bf8c8f437f032edd9ad7a26b94f93a7ea7f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88454483"
---
# <a name="configurationsetting-method---listreservedurls"></a>Metodo di ConfigurationSetting - ListReservedURLs
  Elenca gli URL riservati per tutte le applicazioni presenti nel server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub ListReservedUrls(ByRef Application() as String, ByRef UrlString() as String, _  
    ByRef Account() as String, ByRef AccountSID() as String, _  
    ByRef length() as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListReservedUrls(out string[] Application, out string[] UrlString,  
        out string[] Account, out string[] AccountSID,  
        out int[] Length, out int[] HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Application[]*  
 [out] Applicazioni che dispongono di prenotazioni URL.  
  
 *UrlString[]*  
 [out] URL riservati.  
  
 *Account[]*  
 [out] Nomi account associati all'account per le prenotazioni URL.  
  
 *AccountSID[]*  
 [out] SID di account associati all'account per le prenotazioni URL.  
  
 *Lunghezza*  
 [out] Lunghezza delle matrici restituite dal metodo.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Osservazioni  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
