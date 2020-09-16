---
description: Metodo ListReportServersInDatabase (MSReportServer_ConfigurationSetting WMI)
title: Metodo ListReportServersInDatabase (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 67d5ee6e505a706248490f9fb6c74913657cd455
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480623"
---
# <a name="configurationsetting-method---listreportserversindatabase"></a>Metodo ConfigurationSetting - ListReportServersInDatabase
  Restituisce l'elenco di installazioni del server di report presenti nel database del server di report, indipendentemente dal fatto che tali installazioni accedano a informazioni protette.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parametri  
 *MachineNames[]*  
 [out] Matrice che contiene i nomi di computer per le installazioni del server di report nel database.  
  
 *InstanceNames[]*  
 [out] Matrice che contiene i nomi delle istanze di ognuna delle installazioni del server di report nel database.  
  
 *InstallationIDs[]*  
 [out] Matrice che contiene gli ID di installazione di ogni installazione del server di report nel database.  
  
 *IsInitialized[]*  
 [out] Matrice che contiene lo stato di inizializzazione di ogni installazione del server di report nel database.  
  
 *Lunghezza*  
 [out] Lunghezza delle matrici restituite dal metodo. Tutte le matrici restituite hanno la stessa lunghezza.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
 *ExtendedErrors[]*  
 [out] Matrice di stringhe che contiene errori aggiuntivi restituiti dalla chiamata.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Osservazioni  
 ListReportServersInDatabase elenca le installazioni del server di report presenti nel database del server di report, indipendentemente dal fatto che tali installazioni accedano a informazioni protette e restituisce un set di matrici corrispondente in cui sono contenute le informazioni su ciascuna installazione.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
