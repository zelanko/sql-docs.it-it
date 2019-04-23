---
title: Metodo ListReportServersInDatabase (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: eeb8b39355eac3526fa42aea08df33b32c70472a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59957987"
---
# <a name="listreportserversindatabase-method-wmi-msreportserverconfigurationsetting"></a>Metodo ListReportServersInDatabase (MSReportServer_ConfigurationSetting WMI)
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
  
## <a name="remarks"></a>Note  
 ListReportServersInDatabase elenca le installazioni del server di report presenti nel database del server di report, indipendentemente dal fatto che tali installazioni accedano a informazioni protette e restituisce un set di matrici corrispondente in cui sono contenute le informazioni su ciascuna installazione.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
