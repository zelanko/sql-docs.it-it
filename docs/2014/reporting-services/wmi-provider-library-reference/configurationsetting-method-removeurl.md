---
title: Metodo RemoveURL (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: c9ab7dc3ea75201bd011b85f80169d50e2ba0d37
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52518887"
---
# <a name="removeurl-method-wmi-msreportserverconfigurationsetting"></a>Metodo RemoveURL (MSReportServer_ConfigurationSetting WMI)
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
  
 *Errore*  
 [out] Descrizione dell'errore che si è verificato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Note  
 *UrlString* non include il nome della directory virtuale. A tale scopo è disponibile il [metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-setvirtualdirectory.md).  
  
 Prima di chiamare il metodo [ReserveURL](configurationsetting-method-reserveurl.md) , è necessario specificare un valore per la proprietà di configurazione VirtualDirectory relativa al parametro *Applicazione* . Usare il [Metodo SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting WMI&#41;](configurationsetting-method-setvirtualdirectory.md) per impostare la proprietà VirtualDirectory.  
  
 Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ha reso disponibile un Certificato SSL e nessun altro URL lo richiede, il certificato verrà rimosso.  
  
 Tramite questo metodo tutti i domini di applicazione non relativi alla configurazione eseguono un riciclo pesante e si arrestano durante questa operazione; una volta completata l'operazione, i domini di applicazione vengono riavviati.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
