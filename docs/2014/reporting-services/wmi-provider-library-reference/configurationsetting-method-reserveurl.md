---
title: Metodo ReserveURL (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ReservedURL method
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 2b771042ca00c9a9a80d7ffa035b100e2c4a6dc0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020512"
---
# <a name="reserveurl-method-wmi-msreportserverconfigurationsetting"></a>Metodo ReserveURL (MSReportServer_ConfigurationSetting WMI)
  Aggiunge una prenotazione URL per un'applicazione specifica.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Applicazione*  
 Nome dell'applicazione per la quale riservare l'URL.  
  
 *URLString*  
 URL per la prenotazione.  
  
 *lcid*  
 Impostazioni locali da utilizzare per i messaggi di errore restituiti.  
  
 *Errore*  
 [out] Descrizione dell'errore che si è verificato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Note  
 *UrlString* non include il nome della directory virtuale. A tal fine, viene fornito il metodo [SetVirtualDirectory](configurationsetting-method-setvirtualdirectory.md) .  
  
 Le prenotazioni URL vengono create per l'account del servizio Windows corrente. La modifica dell'account del servizio Windows richiede l'aggiornamento manuale di tutte le prenotazioni URL.  
  
 Questo metodo causa l'esecuzione dell'operazione di riciclo pesante da parte di tutti i domini applicazione. Una volta completata l'operazione, i domini applicazione vengono riavviati.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
