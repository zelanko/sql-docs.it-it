---
title: Metodo DeleteEncryptedInformation (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- DeleteEncryptedInformation (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- DeleteEncryptedInformation method
ms.assetid: c14ed187-bdd9-4304-88e3-72072f03c21b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4ffe9834ea57f3f4a0d48387f631ae08a45182ad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66098515"
---
# <a name="deleteencryptedinformation-method-wmi-msreportserverconfigurationsetting"></a>Metodo DeleteEncryptedInformation (MSReportServer_ConfigurationSetting WMI)
  Elimina le informazioni crittografate dal database del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub DeleteEncryptedInformation(ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void DeleteEncryptedInformation(out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parametri  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
 *ExtendedErrors[]*  
 [out] Matrice di stringhe che contiene errori aggiuntivi restituiti dalla chiamata.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
 Quando viene richiamato questo metodo, i seguenti dati vengono eliminati:  
  
-   Informazioni sulle origini dati crittografate, tra cui nome utente e password.  
  
-   Dati della sottoscrizione crittografati tramite le interfacce dell'estensione per il recapito.  
  
-   Tutte le informazioni della tabella delle chiavi nel database del server di report.  
  
 Una volta richiamato questo metodo, l'utente deve inizializzare ogni computer che utilizza il database del server di report.  
  
 La chiamata al metodo DeleteEncryptedInformation non influisce sul file di configurazione del server di report.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
