---
title: Metodo SetSecureConnectionLevel (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- SetSecureConnectionLevel (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- SetSecureConnectionLevel method
ms.assetid: 0fac7d5e-2670-4657-9439-331e7d93babb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5318d25ed1e6113e65f6e41d40add3ff0203856c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580994"
---
# <a name="configurationsetting-method---setsecureconnectionlevel"></a>Metodo ConfigurationSetting - SetSecureConnectionLevel
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
  
## <a name="remarks"></a>Remarks  
 Quando viene chiamata, la proprietà SecureConnectionLevel del server di report è impostata sul valore specificato. Il valore 0 indica che SSL è disattivato. Il valore maggiore di o pari a 1 indica che SSL è abilitato.  
  
-   Quando il valore è impostato, l'elemento SecureConnectionLevel del file di configurazione del server di report viene modificato e l'elemento **URLRoot** del file di configurazione viene impostato per usare "https://" se il valore specificato per *Level* è maggiore o uguale a 1 oppure "http://" se il valore specificato per *Level* è 0.  
  
 In [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]SecureConnectionLevel diventa un'opzione di attivazione/disattivazione. Il valore predefinito è 0. Per qualsiasi valore maggiore o uguale a 1 passato tramite l'API del metodo SetSecureConnectionLevel, SSL viene considerato abilitato e la proprietà di configurazione SecureConnectionLevel viene impostata di conseguenza nel file rsreportserver.config. I valori 2 e 3 sono ancora consentiti per la compatibilità con le versioni precedenti.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
