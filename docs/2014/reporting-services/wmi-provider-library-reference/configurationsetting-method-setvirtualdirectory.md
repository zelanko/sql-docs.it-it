---
title: Metodo SetVirtualDirectory (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f20db632f41024cc3246eeaff93a41ff2cb713ed
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56016072"
---
# <a name="setvirtualdirectory-method-wmi-msreportserverconfigurationsetting"></a>Metodo SetVirtualDirectory (MSReportServer_ConfigurationSetting WMI)
  Imposta il nome della directory virtuale di una determinata applicazione.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Applicazione*  
 Nome dell'applicazione per cui impostare la directory virtuale.  
  
 *VirtualDirectory*  
 Nome della directory virtuale.  
  
 *lcid*  
 ID impostazioni locali della directory virtuale.  
  
 *Errore*  
 [out] Descrizione dell'errore che si è verificato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Note  
 Un'applicazione può disporre di un solo nome della directory virtuale per tutte le prenotazioni URL.  
  
 VirtualDirectory deve essere conforme alle convenzioni di denominazione per le directory virtuali. VirtualDirectory non deve essere stringa vuota o spazio vuoto.  
  
 Aggiorna il valore dell'elemento \Configuration\URLReservations\Application\VirtualDirectory. Ha esito positivo anche se non è stata ancora creata alcuna prenotazione URL.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
