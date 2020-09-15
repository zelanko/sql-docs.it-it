---
description: Metodo RemoveURL (MSReportServer_ConfigurationSetting WMI)
title: Metodo RemoveURL (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 69112a88d00af4c82e10471addc32eff6d3e7cde
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88423155"
---
# <a name="configurationsetting-method---removeurl"></a>Metodo di ConfigurationSetting - RemoveURL
  Rimuove un URL riservato per il server di report. Se è necessario rimuovere più URL, devono essere rimossi uno per volta chiamando questa API.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Applicazione*  
 Nome dell'applicazione per cui rimuovere la prenotazione.  
  
 *URLString*  
 URL per la prenotazione.  
  
 *lcid*  
 Impostazioni locali da utilizzare per i messaggi di errore restituiti.  
  
 *Error (Errore) (Error (Errore)e)*  
 [out] Descrizione dell'errore che si è verificato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Osservazioni  
 *UrlString* non include il nome della directory virtuale. A tale scopo è disponibile il [metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md).  
  
 Prima di chiamare il metodo [ReserveURL](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md) , è necessario specificare un valore per la proprietà di configurazione VirtualDirectory relativa al parametro *Applicazione* . Usare il [Metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) per impostare la proprietà VirtualDirectory.  
  
 Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ha reso disponibile un certificato TLS/SSL e nessun altro URL lo richiede, il certificato verrà rimosso.  
  
 Tramite questo metodo tutti i domini di applicazione non relativi alla configurazione eseguono un riciclo pesante e si arrestano durante questa operazione; una volta completata l'operazione, i domini di applicazione vengono riavviati.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
