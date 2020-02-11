---
title: Metodo RemoveSSLCertificateBindings (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- RemoveSSLCertificateBindings method
ms.assetid: b8b484c9-04c4-4ae9-980e-67bbe5aa8481
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 4c3e943bcf63f4bcdff22d5425bf474d8aa4d80d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66098183"
---
# <a name="removesslcertificatebindings-method-wmi-msreportserver_configurationsetting"></a>Metodo RemoveSSLCertificateBindings (MSReportServer_ConfigurationSetting WMI)
  Rimuove un'associazione certificato SSL.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub RemoveSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveSSLCertificateBindings(string Application,  
    string CertificateHash, string IPAddress, Int32 Port, Int32 Lcid,  
    out string Error, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *Applicazione*  
 Nome dell'applicazione per la quale l'associazione certificato deve essere rimossa.  
  
 *CertificateHash*  
 Hash per il certificato.  
  
 *IPAddress*  
 Indirizzo IP per l'applicazione.  
  
 *Porta*  
 Porta SSL associata all'associazione.  
  
 *LCID*  
 Impostazioni locali da utilizzare per i messaggi di errore restituiti.  
  
 *Error (Errore) (Error (Errore)e)*  
 [out] Descrizione dell'errore che si è verificato.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Il valore 0 indica l'esito positivo della chiamata al metodo, mentre un codice di errore ne indica l'esito negativo.  
  
## <a name="remarks"></a>Osservazioni  
 Questo metodo rimuove l'associazione specifica dal file rsreportserver.config e facoltativamente da HTTP.SYS.  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
