---
title: Metodo ListReservedURLs (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListReservedURLs method
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e6d4cf7f550db88a56b7906fb4487b6c33935636
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098271"
---
# <a name="listreservedurls-method-wmi-msreportserverconfigurationsetting"></a>Metodo ListReservedURLs (MSReportServer_ConfigurationSetting WMI)
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
  
## <a name="remarks"></a>Note  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
