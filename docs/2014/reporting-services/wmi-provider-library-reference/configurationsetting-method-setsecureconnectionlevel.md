---
title: Metodo SetSecureConnectionLevel (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ede290f794ab61dac62c39bc47b80516385474fa
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097961"
---
# <a name="setsecureconnectionlevel-method-wmi-msreportserver_configurationsetting"></a>Metodo SetSecureConnectionLevel (MSReportServer_ConfigurationSetting WMI)
  Imposta il livello di connessione protetta del server di report.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub SetSecureConnectionLevel(Level as Integer, _  
    ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Int32 Level,   
    out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Level*  
 Valore intero che rappresenta un livello di connessione protetta.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Osservazioni  
 Quando viene chiamata, la proprietà SecureConnectionLevel del server di report è impostata sul valore specificato. Il valore 0 indica che SSL è disattivato. Il valore maggiore di o pari a 1 indica che SSL è abilitato.  
  
-   Quando il valore è impostato, l'elemento SecureConnectionLevel nel file di configurazione del server di report viene modificato e `URLRoot` l'elemento nel file di configurazione viene impostato per utilizzare "https://" Se il *livello* specificato è maggiore o uguale a 1 oppure "http://" Se il *livello* specificato è 0.  
  
 In [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]SecureConnectionLevel diventa un'opzione di attivazione/disattivazione. Il valore predefinito è 0. Per qualsiasi valore maggiore o uguale a 1 passato tramite l'API del metodo SetSecureConnectionLevel, SSL viene considerato abilitato e la proprietà di configurazione SecureConnectionLevel viene impostata di conseguenza nel file rsreportserver.config. I valori 2 e 3 sono ancora consentiti per la compatibilità con le versioni precedenti.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
