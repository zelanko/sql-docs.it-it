---
title: Metodo ListSSLCertificateBindings (MSReportServer_ConfigurationSetting WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListSSLCertificateBindings method
ms.assetid: d12d280c-9b6f-47a8-bcd9-34cde31c8886
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9802176b5f5c82ba60a4e47d85445b54eaa1a5f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031622"
---
# <a name="listsslcertificatebindings-method-wmi-msreportserverconfigurationsetting"></a>Metodo ListSSLCertificateBindings (MSReportServer_ConfigurationSetting WMI)
  Restituisce un elenco dei certificati SSL installati presenti nel computer.  
  
## <a name="syntax"></a>Sintassi  
  
```vb  
Public Sub ListSSLCertificateBindings(ByVal LCID As Int32, ByRef Application() As String, _  
    ByRef CertificateHash() As String, ByRef IPAddresses() As String, ByRef Port() As Int32, _  
    ByRef Errors() As String, ByRef Length As Int32, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListSSLCertificateBindings(Int32 Lcid, out string[] Application,   
    out string[] CertificateHash,out string[] IPAddress,   
    out Int32[] Port, out string Errors,   
    out Int32 length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parametri  
 *LCID*  
 Impostazioni locali da utilizzare per i messaggi di errore restituiti.  
  
 *Application[]*  
 [out] Applicazioni che dispongono di associazioni certificato.  
  
 *CertificateHash[]*  
 [out] Hash per i certificati.  
  
 *IPAddress[]*  
 [out] Indirizzo IP per le applicazioni.  
  
 *Port[]*  
 [out] Numero di porta archiviato nell'associazione in rsreportserver.config.  
  
 *Errors[]*  
 [out] Descrizioni degli errori che si sono verificati.  
  
 *Lunghezza*  
 [out] Lunghezza della matrice restituita dal metodo.  
  
 *HRESULT*  
 [out] Valore che indica se la chiamata ha avuto esito positivo o negativo.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un *HRESULT* che indica l'esito positivo o negativo della chiamata al metodo. Un valore pari a 0 indica l'esito positivo della chiamata al metodo. Un valore diverso da zero indica che si è verificato un errore.  
  
## <a name="remarks"></a>Note  
  
## <a name="requirements"></a>Requisiti  
 **Spazio dei nomi:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Membri di MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
